# Contents

- [Kotlin](#kotlin)
  - [Diagram Elements](#diagram-elements)
  - [Method Calling](#method-calling)
  - [Screen/ViewModel Relationship](#screenviewmodel-relationship)
  - [Implementation](#implementation)
  - [Aggregation](#aggregation)
  - [Composition](#composition)
  - [Aggregation With `List`](#aggregation-with-list)
  - [Composition With `Flow` of a `List`](#composition-with-flow-of-a-list)

- [Swift](#swift)
  - [Diagram Elements](#diagram-elements-swift)
  - [Method Calling](#method-calling-swift)
  - [Screen/ViewModel Relationship](#screenviewmodel-relationship-swift)
  - [Implementation](#implementation-swift)
  - [Aggregation](#aggregation-swift)
  - [Composition](#composition-swift)
  - [Aggregation With `Array`](#aggregation-with-array)
  - [Composition With `AnyPublisher` of an `Array` of `Pair`](#composition-With-AnyPublisher-of-an-array-of-pair)
  - [UI State Pattern](#ui-state-pattern)

# Kotlin
## Diagram Elements
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/diagram-elements.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/kotlin/diagram-elements.light.svg">
</picture>

## Method Calling
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/method-calling.dark.svg">
  <img alt="Method Calling Diagram Diagram" src="./res/kotlin/method-calling.light.svg">
</picture>

```kotlin
@HiltViewModel
class HomeViewModel @Inject constructor(private val homeRepository: HomeRepository) : ViewModel() {
    fun addURIs(uris: List<String>) = viewModelScope.launch {
        homeRepository.addURIs(uris = uris)
    }
}
```

## Screen/ViewModel Relationship
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/screen-viewmodel-relationship.dark.svg">
  <img alt="Screen ViewModel Relationship" src="./res/kotlin/screen-viewmodel-relationship.light.svg">
</picture>

```kotlin
// NavGraphBuilderExtension.kt

@Composable
fun NavGraphBuilder.administrativeUnitsScreen(/*..*/) {
  val viewModel = hiltViewModel<AdministrativeUnitsViewModel>()
  val administrativeUnitsUiState by viewModel
    .administrativeUnitsUiStateFlow
    .collectAsState(initial = AdministrativeUnitsUiState.Loading)
  /*...*/

  AdministrativeUnitsScreen(
    /*...*/
    administrativeUnitsUiState = administrativeUnitUiState
    onAdministrativeUnitPressedAt = viewModel::onAdministrativeUnitPressedAt
    /*...*/
  )
}
```

## Implementation
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/implementation.dark.svg">
  <img alt="Implementation Diagram" src="./res/kotlin/implementation.light.svg">
</picture>

```kotlin
class ImageRoomDataSource : ImageDataSource { /*...*/ }
```

## Aggregation
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/aggregation.dark.svg">
  <img alt="Aggregation Diagram" src="./res/kotlin/aggregation.light.svg">
</picture>

```kotlin
data class Region(
    val boundingBox: BoundingBox
)
```

## Composition
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/composition.dark.svg">
  <img alt="Composition Diagram" src="./res/kotlin/composition.light.svg">
</picture>

```kotlin
data class Region(
    val active: Boolean = true
)
```

## Aggregation With `List`
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/aggregation-list.dark.svg">
  <img alt="Aggregation With List Diagram" src="./res/kotlin/aggregation-list.light.svg">
</picture>

```kotlin
data class Region(
   private val holes : List<Polygon>
)
```

## Composition With `Flow` of a `List`
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/kotlin/dark/composition-flow-list.dark.svg">
  <img alt="Composition With Flow of a List" src="./res/kotlin/composition-flow-list.light.svg">
</picture>

```kotlin
class AdministrativeUnitsRepository {
    private var administrativeUnits: List<AdministrativeUnit> = emptyList()
}
```

# Swift
## Diagram Elements (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/diagram-elements.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/swift/diagram-elements.light.svg">
</picture>

## Method Calling (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/method-calling.dark.svg">
  <img alt="Method Calling Diagram" src="./res/swift/method-calling.light.svg">
</picture>

```swift
class ConversationsViewModel: ObservableObject {
    private let conversationsRepository: ConversationsRepository

    /*...*/

    func selectContact(of id: String) {
        /*...*/
        conversationsRepository.selectContact(of: id)
    }
}
```

## Screen/ViewModel Relationship (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/screen-viewmodel-relationship.dark.svg">
  <img alt="Screen ViewModel Relationship" src="./res/swift/screen-viewmodel-relationship.light.svg">
</picture>

```swift
struct Navigation {
  @EnvironmentObject var conversationViewModel: ConversationViewModel
  /*...*/

  var body: some View {
    /*...*/
    let conversationsScreen = ConversationsScreen(
        contactWithLastMessageListUIState: $conversationsViewModel
            .contactWithLastMessageListUIState,
        /*...*/
        selectConversationWith: conversationsViewModel.selectConversation(with:),
      )
  }
}
```

## Implementation (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/implementation.dark.svg">
  <img alt="Implementation Diagram" src="./res/swift/implementation.light.svg">
</picture>

```swift
class MessengerBluetoothDataSource: MessengerDataSource 
```

## Aggregation (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/aggregation.dark.svg">
  <img alt="Aggregation Diagram" src="./res/swift/aggregation.light.svg">
</picture>

```swift
struct Conversation {
    let contact: Contact
}
```

## Composition (swift)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/composition.dark.svg">
  <img alt="Composition Diagram" src="./res/swift/composition.light.svg">
</picture>

```swift
struct MessageViewData {
    let id: UUID = UUID()
}
```

## Aggregation With `Array`
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/aggregation-array.dark.svg">
  <img alt="Aggregation With List Diagram Swift" src="./res/swift/aggregation-array.light.svg">
</picture>

```swift
struct Conversation {
    var messages: [Message]
}
```

## Composition With `AnyPublisher` of an `Array` of `Pair`
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/composition-anypublisher-array-of-pair.dark.svg">
  <img alt="Composition With AnyPublisher of an Array of Pair" src="./res/swift/composition-anypublisher-array-of-pair.light.svg">
</picture>

```swift
struct ConversationsRepository {
    var contactWithLastMessageListPublisher: AnyPublisher<[(Contact, Message)], Never> {
      /*...*/
    }
}
```

## UI State Pattern
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/swift/dark/ui-state-pattern.dark.svg">
  <img alt="UI State Pattern" src="./res/swift/ui-state-pattern.svg">
</picture>

```swift
enum ContactWithLastMessageListUIState {
    case loading
    case contactWithLastMessageListLoaded([(ContactViewData, MessageViewData)])
}
```
