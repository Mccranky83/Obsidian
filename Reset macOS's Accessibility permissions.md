```bash
sudo tccutil reset Accessibility com.example.app
```
`tccutil` stands for "Transparency, Consent, and Control Utility".

The `com.example.app` part is the specified app's bundle-id. In order the get the id, fetch it with AppleScript via the `osascript` command:
```bash
osascript -e 'id of app "Example Appname"'
```