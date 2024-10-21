# Uncomment the next line to define a global platform for your project
platform :ios, '13.0'
def dependency_pods
  # Pods for ktp.usurp.ios
  pod 'Locksmith'
  pod 'JSONWebToken', :git => 'https://github.com/radianttap/JSONWebToken.swift.git', :branch => 'podspec'
  pod 'SVProgressHUD'
  pod 'FMDB'
  pod 'UICircularProgressRing'
  pod 'RxSwift'
  pod 'RxCocoa'
  pod 'NotificationBannerSwift', '2.0.1'
  pod 'AEXML'
  pod 'Mixpanel','3.6.2'
  pod 'Brightcove-Player-Core', :source => 'https://github.com/brightcove/BrightcoveSpecs.git'
  pod 'JWTDecode'
  pod 'Firebase/Analytics'
  pod 'Firebase/Crashlytics'
  pod 'Firebase/Messaging'
  pod 'Apollo', '1.0.6'
  
  
end
use_frameworks!
target 'medical' do
  dependency_pods
end
target 'pance' do
  dependency_pods
end
target 'mcat' do
  dependency_pods
end
target 'ppi' do
  dependency_pods
end
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings["IPHONEOS_DEPLOYMENT_TARGET"] = "13.0"
    end
    if ['ReSwift'].include? target.name
      target.build_configurations.each do |config|
        config.build_settings['SWIFT_VERSION'] = '4.2'
      end
    end
  end
end
