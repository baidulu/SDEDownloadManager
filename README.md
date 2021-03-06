

<p align="center">

<img src="https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/ICON.png" alt="SDEDownloadManager" title="SDEDownloadManager" width="100"/>

</p>

`SDEDownloadManager` is a download management library, which is written with Swift and is compatible with Objective-C.

The same name class [SDEDownloadManager](https://seedante.github.io/SDEDownloadManager/Classes/SDEDownloadManager.html) provides download management features. And, a UITableViewController subclass, [DownloadListController](https://seedante.github.io/SDEDownloadManager/Classes/DownloadListController.html), coordinates with [SDEDownloadManager](https://seedante.github.io/SDEDownloadManager/Classes/SDEDownloadManager.html) to display and manage download tasks, and track download activity.

[API Reference](https://seedante.github.io/SDEDownloadManager/): Quick help in Xcode maybe doesn't work well out of framework, you will need this. It's generated by [jazzy](https://github.com/realm/jazzy).

## Requirements

* iOS 8.0/Swift 4.0


## Library Components

#### SDEDownloadManager <sub>[[Document]](https://seedante.github.io/SDEDownloadManager/Classes/SDEDownloadManager.html)

* Basic download management: download/pause/resume/stop/restart/delete.
* Sort download list with predefine types and powerful predicate.
* Control download count: it's good as you think.
* Track download activity: download progress and speed.
* Cache thumbnails for files.
* Handle part authentication: Basic, Digest, and server trust.
* Handle app force quit in downloading and you have to do nothing.

The features it **doesn't support**:

* Don't support specifying file store location. It's meaningless on iOS devices.
* Don't support playing and caching online media file. It just download file.
* Don't support limiting download speed.
* Don't support multithreading download for a single file.


#### DownloadListController <sub>[[Document]](https://seedante.github.io/SDEDownloadManager/Classes/DownloadListController.html) [[Cheat Sheet]](https://github.com/seedante/SDEDownloadManager/wiki/Cheat-Sheet)

* Custom content to display:
 
 ![](https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/DownloadListType.png)
 
* Custom cell content. All elements in the cell are customizable, some examples:

  ![](https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/CellTypeA.png)
  ![](https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/CellTypeB.png)
  ![](https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/CellTypeC.png)
  Except textLabel, other elements could be hidden. 
  
  You also could use custom UITableViewCell. There is only one cell available for now.
  
* Custom manage features in cell swipe and multiple selection, these features are disabled by default;
* Adjust max download count by `adjustButtonItem`;
* Sort list by `sortButtonItem`.
![](https://raw.githubusercontent.com/seedante/iOS-Note/master/SDEDownloadManager/Swipe.CDC.Sort.png)

#### SliderAlertController <sub>[[Document]](https://seedante.github.io/SDEDownloadManager/Classes/SliderAlertController.html)

A UIViewController subclass like UIAlertController to display a slider, allows to display custom symbol for special vaule, like "∞" for 0 above.

#### URLPickerController <sub>[[Document]](https://seedante.github.io/SDEDownloadManager/Classes/URLPickerController.html)

A UITableViewController subclass to pick URL strings. In demo, I use it to pick files for `DownloadListController` to download.

   
## What you need to know before using the library

`SDEDownloadManager` maintains a `downloadList` for all tasks, which is a `[[String]]`and is designed for UITableView/UICollectionView.

Here is the only method to create a SDEDownloadManager object:

    static func manager(identifier: String, manualMode: Bool = false) -> SDEDownloadManager
    
If a download manager with specified identifier exists in the memory already, this method returns it directly, so you don't have to keep a reference to use it in other places.

    let libraryLink = "https://codeload.github.com/seedante/SDEDownloadManager/zip/master"
    SDEDownloadManager.manager(identifier: "Link").download([libraryLink])


SDEDownloadManager has two sort modes: manual and predefined mode(include: `.addTime`, `.fileName`, `.fileSize`, `.fileType`). The two sort modes can switch to each other freely in `sortListBy(type:order:)`. Except for obvious sort difference, what's difference between with two modes?

1. Download new file. In predefined mode, you just need to offer download URL, but in manual mode, you must also offer its insert location in `downloadList`. 

2. A section in UITableView with `.plain` style can't be distinguished from last section if it doesn't have a title, so in manual mode, when you insert a new section, it must have a title.

Although you can switch between with two sort modes freely, switching from manual mode to predefined mode will lose all section titles, and switching from predefined mode to manual mode will integrate all tasks into one section with a placeholder title, so choose sort mode based on your usage scenario discreetly.

In addition, in predefined mode, when downloading a new file, its name and type maybe change, and its file size is known after its meta info is fetched, so SDEDownloadManager change its sort type to `.addTime` automatically if it's not.


## Installation

CocoaPods: `pod 'SDEDownloadManager'`

Carthage: `github "seedante/SDEDownloadManager"`

If you are not familiar with CocoaPods or Carthage, or you want to install it manually, reference to [Installation Guide](https://github.com/seedante/SDEDownloadManager/wiki/Installation-Guide).

After installation, import SDEDownloadManager into your project:

    // In Swift file
    import SDEDownloadManager
    // In Objective-C file
    @import SDEDownloadManager;


## Localization for UIViewController in the Library

Supported localizable languages for now: English, Simplified Chinese.

## License

SDEDownloadManager is released under the [MIT LICENSE](https://github.com/seedante/SDEDownloadManager/blob/master/LICENSE).