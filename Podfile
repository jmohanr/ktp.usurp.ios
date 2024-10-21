platform :ios, '13.0'
use_frameworks!

# Function to set run script to always run when no input/output files exist
def set_run_script_to_always_run_when_no_input_or_output_files_exist(project:)
  project.targets.each do |target|
    run_script_build_phases = target.build_phases.select { |phase| phase.is_a?(Xcodeproj::Project::Object::PBXShellScriptBuildPhase) }
    cocoapods_run_script_build_phases = run_script_build_phases.select { |phase| phase.name && phase.name.start_with?("[CP]") }
    
    cocoapods_run_script_build_phases.each do |run_script|
      if (run_script.input_paths || []).empty? && (run_script.output_paths || []).empty?
        run_script.always_out_of_date = "1" # Ensure it runs always if inputs/outputs are missing
      end
    end
  end
  project.save
end

post_integrate do |installer|
  main_project = installer.aggregate_targets[0].user_project
  set_run_script_to_always_run_when_no_input_or_output_files_exist(project: main_project)
end

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
  pod 'Mixpanel', '3.6.2'
  pod 'Brightcove-Player-Core', :source => 'https://github.com/brightcove/BrightcoveSpecs.git'
  pod 'JWTDecode'
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

  # Ensure run scripts without input/output files are always run
  installer.aggregate_targets.each do |aggregate_target|
    set_run_script_to_always_run_when_no_input_or_output_files_exist(project: aggregate_target.user_project)
  end
end
