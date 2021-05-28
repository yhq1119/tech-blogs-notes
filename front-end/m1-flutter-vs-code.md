M1 Apple Mac Mini

cannot detect iOS simulator - Xcode installation incomplete

**Solution:**

found that this fix solves the issue: http://stackoverflow.com/questions/17980759/xcode-select-active-developer-directory-error

1.Install Xcode (get it from https://developer.apple.com/xcode/) if you don't have it yet.
Accept the Terms and Conditions.

2.Ensure Xcode app is in the /Applications directory (NOT /Users/{user}/Applications).
Point xcode-select to the Xcode app Developer directory using the following command:
```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```
Run 
```
flutter doctor
``` 
all fixed.
