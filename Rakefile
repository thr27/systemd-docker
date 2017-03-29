require 'timber'

namespace :ops do
  TINFOIL_GITHUB = 'git@github.com:tinfoil/systemd-docker.git'.freeze
  VERSION_FILE_PATH = '.release-version'

  if defined?(Timber)
    timber_options = {
      version_file_path: VERSION_FILE_PATH,
      github_repo:       TINFOIL_GITHUB
    }

    if ENV['JIRA_URL'] &&
       ENV['JIRA_USERNAME'] &&
       ENV['JIRA_PASSWORD']
      timber_options[:jira] = {
        url:        ENV['JIRA_URL'],
        username:   ENV['JIRA_USERNAME'],
        password:   ENV['JIRA_PASSWORD']
      }
    end

    Timber::Tasks::Release.new(timber_options)
  end
end

task default: [:clean, :deps, :build]

task :clean do
  system 'go clean'
end

task :deps do
  system 'glide install'
end

task :build do
  system './build'
end
