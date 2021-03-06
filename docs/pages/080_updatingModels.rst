Updating Models
===============

Whenever a model is updated, Rocket Data will automatically update any models or child models which need updating. If you use the Model protocol, all subtrees will always be kept in sync. There are several ways which can trigger updates:

  1. Any time a DataProvider or CollectionDataProvider is mutated, any new models are considered updated.
  2. The DataModelManager has specific methods to update a model or array of models.
  3. The DataModelManager also has a method to delete a model from both the cache and any model which contains this deleted model.

Most of these updates happen asynchronously, so other data providers won't be updated in the same main thread block. However, these updates nearly always happen extremely quickly (~1 ms), so you don't need to worry about this. Updates are asynchronous to ensure that Rocket Data never blocks the main thread and never slows down your app, regardless of the number of models or data providers you use.

Conflicts
---------

Since updates are asynchronous, it is possible to have conflicts. There are automatically resolved by the library by always picking the most recent change. The library keeps track of a change time for all changes. If a change was initiated at a change time in the past, it is discarded.
