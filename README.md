# Swift Tips & tricks
Here's list of Swift tips & tricks that I would like to share.
下記はよく使うSwiftのゴードで、ぜひ参考してください；）

## Table of contents

[#1 Handle safe area of iPhoneX](https://github.com/Jack7a5aGitHub/iOS_SwiftTipsAndUsefulCode#1-Handle-safe-area-of-iPhoneX)<br />
[#2 Handle Tab Bar Indicator](https://github.com/Jack7a5aGitHub/iOS_SwiftTipsAndUsefulCode#2-Handle-Tab-Bar-Indicator)<br />
[#3 Collection Scroll](https://github.com/Jack7a5aGitHub/iOS_SwiftTipsAndUsefulCode#3-Collection-Scroll)<br />
[#4 Responsive TextField](https://github.com/Jack7a5aGitHub/iOS_SwiftTipsAndUsefulCode#4-Responsive-TextField)<br />
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
## [#2 Handle Tab Bar Indicator]()

Add Indicator to Tab bar.

```swift
extension UIImage {
    func createSelectionIndicator(color: UIColor, size: CGSize, lineWidth: CGFloat) -> UIImage {
        UIGraphicsBeginImageContextWithOptions(size, false, 0)
        color.setFill()
        UIRectFill(CGRect(x: 0, y: size.height - lineWidth, width: size.width, height: lineWidth))
        guard let image = UIGraphicsGetImageFromCurrentImageContext() else {
            return UIImage()
        }
        UIGraphicsEndImageContext()
        return image
    }
}

// Usage 
        self.tabBar.selectionIndicatorImage = UIImage().createSelectionIndicator(color: #colorLiteral(red: 0.07843137255, green: 0.4901960784, blue: 0.7529411765, alpha: 1), size: CGSize(width: tabBar.frame.width / CGFloat(tabBar.items.count), height: tabBar.frame.height), lineWidth: 2.0)
```

## [#3 Collection Scroll]()

To determine cell after scrolling

```swift
 func scrollViewDidEndDecelerating(_ scrollView: UIScrollView) {
        var visibleRect = CGRect()
        visibleRect.origin = servicesCollectionView.contentOffset
        visibleRect.size = servicesCollectionView.bounds.size
        let visiblePoint = CGPoint(x: visibleRect.minX, y: visibleRect.midY)
        guard let indexPath = servicesCollectionView.indexPathForItem(at: visiblePoint) else {
            return
        }
    }
    func scrollViewWillEndDragging(_ scrollView: UIScrollView, withVelocity velocity: CGPoint, targetContentOffset: UnsafeMutablePointer<CGPoint>) {
        var visibleRect = CGRect()
        visibleRect.origin = servicesCollectionView.contentOffset
        visibleRect.size = servicesCollectionView.bounds.size
        let visiblePoint = CGPoint(x: visibleRect.minX, y: visibleRect.midY)
        guard let indexPath = servicesCollectionView.indexPathForItem(at: visiblePoint) else {
            return
        }
    }
```

## [#4 Responsive TextField]()

Update TextField Status

```swift
textField.addTarget(self, action: #selector(textFieldDidChange(_:)), for: .editingChanged)

@objc func textFieldDidChange(_ textField: UITextField) {

}
```
