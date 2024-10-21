platform :ios, '13.0'
use_frameworks!

def dependency_pods
  # Pods for ktp.usurp.ios
  pod 'Locksmith'
  pod 'SVProgressHUD'
  pod 'FMDB'
  pod 'UICircularProgressRing'
  pod 'RxSwift'
  pod 'RxCocoa'
  pod 'NotificationBannerSwift', '2.0.1'
  pod 'AEXML'
  pod 'Mixpanel', '3.6.2'
  pod 'Brightcove-Player-Core', :source => 'https://github.com/brightcove/BrightcoveSpecs.git'
  pod 'Firebase/Analytics'
  pod 'Firebase/Crashlytics'
  pod 'Firebase/Messaging'
  pod 'Apollo', '1.0.6'
end

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
      config.build_settings["IPHONEOS_DEPLOYMENT_TARGET"] = "13.0" # Set deployment target to iOS 13.0
    end

    if ['ReSwift'].include? target.name
      target.build_configurations.each do |config|
        config.build_settings['SWIFT_VERSION'] = '4.2' # Set Swift version for ReSwift
      end
    end
  end
end
