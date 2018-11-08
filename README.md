# Swift Tips & tricks
Here's list of Swift tips & tricks that I would like to share.
下記はよく使うSwiftのゴードで、ぜひ参考してください；）

## Table of contents

[#1 Handle safe area of iPhoneX](https://github.com/Jack7a5aGitHub/iOS_SwiftTipsAndUsefulCode#1-Handle-safe-area-of-iPhoneX)<br />

## [#1 Handle safe area of iPhoneX]()

UIScreen Extension to calculate the height of safe area or width of safe area.

```swift
// Use in viewDidLayoutSubviews()
extension UIScreen {
    func widthOfSafeArea() -> CGFloat {
        guard let rootView = UIApplication.shared.keyWindow else {
            return 0   
        }
        if #available(iOS 11.0, *) {
            let leftInset = rootView.safeAreaInsets.left
            let rightInset = rootView.safeAreaInsets.right
            return rootView.bounds.width - leftInset - rightInset
        } else {
            return rootView.bounds.width   
        }      
    }    
    func heightOfSafeArea() -> CGFloat {    
        guard let rootView = UIApplication.shared.keyWindow else {
            return 0     
        }      
        if #available(iOS 11.0, *) {          
            let topInset = rootView.safeAreaInsets.top           
            let bottomInset = rootView.safeAreaInsets.bottom        
            return topInset + bottomInset
        } else {
            return 0   
        }  
    }
}
```
