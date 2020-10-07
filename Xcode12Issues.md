# Xcode 12 Clang: Error in PodSpec Validation due to architectures

## To resolve above issue do the following:

Choose the right section to resolve it on your side.

> For SDK owners:

The solution is to open the podspec and add below:

```ruby
s.pod_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64'}
s.user_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64'}
s.ios.deployment_target  = '10.0' // not required
```

> For SDK users:

1. Navigate to Build Settings of your project and add Any iOS Simulator SDK with value arm64 inside Excluded Architecture.

![image](https://user-images.githubusercontent.com/3921852/95323083-3dd69b00-08a6-11eb-9648-b69f47b10494.png)

2. On Podfile add:

```ruby
post_install do |installer|
  installer.pods_project.build_configurations.each do |config|
    config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
  end
end
```

