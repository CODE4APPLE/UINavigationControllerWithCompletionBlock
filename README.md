NavigationControllerWithBlocks
==============================

The UINavigationController missing methods ! (push / pop with optional completionBlock). 
The implementation use the navigationController delegate on UINavigationController itself.


This project provides : 
* A completionBlock to manage your push/pop events,
* A safe way to push/pop multiple controllers at the same times.
```objc

   [self.navigationController popViewControllerAnimated:YES withCompletionBlock:NULL];
   [self.navigationController popViewControllerAnimated:YES withCompletionBlock:NULL];
   [self.navigationController popViewControllerAnimated:YES withCompletionBlock:NULL];
```
* No more "Nested pop animation can result in corrupted navigation bar", 
* No more "Finishing up a navigation transition in an unexpected state. Navigation Bar subview tree might get corrupted."
* No more crash because of deallocated controllers between your multiple animations.

![Image](./screenshots/demo.png)

Added methods 
---------------------------------------------------

```objc
- (void)pushViewController:(UIViewController *)viewController 
                 animated:(BOOL)animated 
      withCompletionBlock:(JMONavCompletionBlock)completionBlock;

- (void)popViewControllerAnimated:(BOOL)animated 
              withCompletionBlock:(JMONavCompletionBlock)completionBlock;
- (void)popToRootViewControllerAnimated:(BOOL)animated
                    withCompletionBlock:(JMONavCompletionBlock)completionBlock;
```

Usage
-------------------------------------------------------------
* using category (UINavigationController+CompletionBlock), just call the method to activate auto delegation.
```objc
- (void)activateCompletionBlock;
```
and use the pop/push methods 
```objc
[self.navigationController popViewControllerAnimated:YES withCompletionBlock:NULL];
[self.navigationController pushViewController:vc animated:YES withCompletionBlock:^(BOOL successful) {
   NSLog(@"Hi ! Push done !");
}];
```

* using JMONavigationController (subclassing UINavigationController), nothing to be done, default initalizers are overided to call activateCompletionBlock.
but use the pop/push methods 
```objc
[self.navigationController popViewControllerAnimated:YES withCompletionBlock:NULL];
[self.navigationController pushViewController:vc animated:YES withCompletionBlock:^(BOOL successful) {
   NSLog(@"Hi ! Push done !");
}];
```

