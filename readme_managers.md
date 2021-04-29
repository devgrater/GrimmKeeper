# The Managers
## 0. Table of Contents

## 1. SmartphoneManager
SmartphoneManager is responsible for:
 - Controlling the visibility of the Smartphone
 - Starting an app, or passing data between apps.
 - For more detail on starting apps or making your own apps, [check here](readme_smartphone_system.md)

### 1.1. Handy Functions in SmartphoneManager
 - `ButtonReturn()`: Simulates a return button press on Android devices. Removes the latest view on queue, and start the new latest view.
 - `StartApp(string appName, string viewID, bool startFresh)`: Starts another app and opens up the view given. If `startFresh`, all apps and views before this will be closed. The newly started view will be the only one on queue. If `startFresh` is set to false, the view is added to the existing queue.
 - `PassData(ViewData data)`: Passes a view data object to the latest view. The latest view's function `PopulateFromViewData()` will pick this up, and populate content based on the data passed.


## 2. MeowwerManager
MeowwerManager is responsible for:
 - Loading Meowts (Tweets in real life) into its meowt base
 - Per request, send Meowts to apps that needs it.
 - For more detail on adding and loading Meowts, [check here](readme_meowt_system.md)

### 2.1. Handy Functions in MeowwerManager
 - `AppendMeowts(string path, bool replaceOriginal = false)`: Reads all meowts from a JSON at the given path, relative to the `Resources` folder, and add to the Meowt registry. If `replaceOriginal`, all meowts before will be removed before appending. Otherwise, the meowt is appended to the bottom of the Meowt list.
 - `GetMeowtUserFromUID(string uid)`: Returns a `MeowtUser` object from the given user id string. If no matches are found, returns `null`
 - `ParseJsonFromPath(string path)`: From the given path, parses a JSON file and returns a `MeowtWrapper` object. The wrapper contains a list of `Meowt` objects in the field `meowts`.
 - `GetMeowts(int count)`: returns the first `count` Meowts in the Meowt registry. If `count` is set to 0, returns the full list.

## 3. SearchManager
SearchManager is responsible for:
 - Loading and indexing webpages
 - Parsing the webpage's detail info (SearchResult.txt)
 - Executing a Search Based on the Given Keywords
 - For more detail on search indexes and adding webpages, [check here](readme_search_system.md)

### 3.1.
