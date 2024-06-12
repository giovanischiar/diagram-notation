# Contents

- [Kotlin](#kotlin)
  - [Diagram Elements](#diagram-elements)
  - [Method Calling](#method-calling)
  - [Screen/ViewModel Relationship](#screenviewmodel-relationship)
  - [Implementation](#implementation)
  - [Aggregation](#aggregation)
  - [Composition](#composition)
  - [Aggregation With List](#aggregation-with-list)
  - [Composition With Mutable Map](#composition-with-mutable-map)
  - [Composition With Pair of Set](#Composition-with-pair-of-set)
- [Swift](#swift)
  - [Diagram Elements](#diagram-elements)
  - [Method Calling](#method-calling)
  - [Screen/ViewModel Relationship](#screenviewmodel-relationship)
  - [Implementation](#implementation)
  - [Aggregation](#aggregation)
  - [Composition](#composition)
  - [Aggregation With Array](#aggregation-with-array)
  - [Composition With Publisher of Pair](#Composition-with-publisher-of-pair)

# Kotlin
## Diagram Elements
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/diagram-elements.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/diagram-elements.light.svg">
</picture>

## Method Calling
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/method-calling.dark.svg">
  <img alt="Method Calling Diagram Diagram" src="./res/method-calling.light.svg">
</picture>

```kotlin
class AppViewModel(private val repository: AppRepository) : ViewModel { 
  /*...*/ 
    suspend fun addURIs(uris: List<String>) {
        repository.addURIs(uris = uris)
    }
}
```

## Screen/ViewModel Relationship
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/screen-viewmodel-relationship.dark.svg">
  <img alt="Screen ViewModel Relationship" src="./res/screen-viewmodel-relationship.light.svg">
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
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/implementation.dark.svg">
  <img alt="Implementation Diagram" src="./res/implementation.light.svg">
</picture>

```kotlin
class MainRepository : HomeRepository { /*...*/ }
```

## Aggregation
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/aggregation.dark.svg">
  <img alt="Aggregation Diagram" src="./res/aggregation.light.svg">
</picture>

```kotlin
data class Region(
   private val boundingBox : BoundingBox
)
```

## Composition
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition.dark.svg">
  <img alt="Composition Diagram" src="./res/composition.light.svg">
</picture>

```kotlin
data class Address(
   private val administrativeUnit : AdministrativeUnit = CITY
)
```

## Aggregation With List
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/aggregation-list.dark.svg">
  <img alt="Aggregation With List Diagram" src="./res/aggregation-list.light.svg">
</picture>

```kotlin
data class Region(
   private val holes : List<Polygon>
)
```

## Composition With Mutable Map
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition-mutable-map.dark.svg">
  <img alt="Composition With Mutable Map Diagram" src="./res/composition-mutable-map.light.svg">
</picture>

```kotlin
class MainRepository {
   private val locationAddress: MutableMap<Address, Location> = /*...*/
}
```

## Composition With Pair of Set
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition-pair-set.dark.svg">
  <img alt="Composition With Pair of Set Diagram" src="./res/composition-pair-set.light.svg">
</picture>

```kotlin
class MainRepository {
   private val currentImages: Pair<Address, Set<Image>>? = /*...*/
}
```

# Swift
## Diagram Elements
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/diagram-elements-swift.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/diagram-elements-swift.light.svg">
</picture>

## Method Calling

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

## Screen/ViewModel Relationship
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

## Implementation
```swift
class MessengerBluetoothDataSource: MessengerDataSource 
```

## Aggregation
```swift
struct Conversation {
    let contact: Contact
}
```

## Composition
```swift
struct MessageViewData {
    let id: UUID = UUID()
}
```

## Aggregation With Array
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/aggregation-list-swift.dark.svg">
  <img alt="Aggregation With List Diagram Swift" src="./res/aggregation-list-swift.light.svg">
</picture>

```swift
struct Conversation {
    var messages: [Message]
}
```

## Composition With AnyPublisher of Pair
```swift
struct ConversationsRepository {
    var contactWithLastMessageListPublisher: AnyPublisher<[(Contact, Message)], Never> {
      /*...*/
    }
}
```