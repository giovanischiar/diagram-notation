### Diagram Elements
## Kotlin
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/diagram-elements.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/diagram-elements.light.svg">
</picture>

## Swift
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/diagram-elements-swift.dark.svg">
  <img alt="Diagram Elements Diagram" src="./res/diagram-elements-swift.light.svg">
</picture>

### Method Calling
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

### Screen/ViewModel Relationship
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/screen-viewmodel-relationship.dark.svg">
  <img alt="Screen ViewModel Relationship" src="./res/screen-viewmodel-relationship.light.svg">
</picture>

```kotlin
@Composable
fun HomeScreen(viewModel: HomeViewModel, /*...*/) {
  /*...*/
  LaunchedEffect(Unit) { viewModel.subscribe() }
  val addressLocationImages by viewModel.addressLocationImages.collectAsState()
  /*...*/
}
```

### Implementation
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/implementation.dark.svg">
  <img alt="Implementation Diagram" src="./res/implementation.light.svg">
</picture>

```kotlin
class MainRepository : HomeRepository { /*...*/ }
```

### Aggregation
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/aggregation.dark.svg">
  <img alt="Aggregation Diagram" src="./res/aggregation.light.svg">
</picture>

```kotlin
data class Region(
   private val boundingBox : BoundingBox
)
```

### Composition
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition.dark.svg">
  <img alt="Composition Diagram" src="./res/composition.light.svg">
</picture>

```kotlin
data class Address(
   private val administrativeUnit : AdministrativeUnit = CITY
)
```

### Aggregation With List
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/aggregation-list.dark.svg">
  <img alt="Aggregation With List Diagram" src="./res/aggregation-list.light.svg">
</picture>

```kotlin
data class Region(
   private val holes : List<Polygon>
)
```

### Composition With Mutable Map
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition-mutable-map.dark.svg">
  <img alt="Composition With Mutable Map Diagram" src="./res/composition-mutable-map.light.svg">
</picture>

```kotlin
class MainRepository {
   private val locationAddress: MutableMap<Address, Location> = /*...*/
}
```

### Composition With Pair of Set
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./res/dark/composition-pair-set.dark.svg">
  <img alt="Composition With Pair of Set Diagram" src="./res/composition-pair-set.light.svg">
</picture>

```kotlin
class MainRepository {
   private val currentImages: Pair<Address, Set<Image>>? = /*...*/
}
```