# If you have OpenSSL installed, we recommend updating
# the following line to use "https"
source 'http://rubygems.org'

gem "middleman", "~> 3.3.12"
gem "middleman-blog", "~> 3.5.3"
gem "middleman-blog-drafts"
gem 'middleman-blog-similar'
gem "middleman-minify-html"
gem "middleman-deploy"
gem "middleman-livereload"
gem "middleman-gh-pages"
gem "middleman-syntax"
gem 'middleman-imageoptim'
gem 'middleman-search_engine_sitemap'
gem 'middleman-sitemap-ping'
gem 'middleman-build-reporter'

# Let me do spellcheck development easily.
if ENV.include?("DEV") then
  File.delete("middleman-spellcheck")
  File.symlink("../middleman-spellcheck", "middleman-spellcheck")
  gem "middleman-spellcheck", '~> 0.8.0', :path => "middleman-spellcheck"
else
  gem "middleman-spellcheck", '~> 0.8.0',
	:git => "https://github.com/wkoszek/middleman-spellcheck.git",
	:branch => "frontmatter_spell"
end

# HTML/CSS stuff.
gem 'bourbon'

# Testing
gem 'capybara'
gem 'selenium-webdriver'
gem "chromedriver-helper", "0.0.6"

# For feed.xml.builder
gem "builder", "~> 3.0"
gem 'rspec'		# spec/ requirement
gem 'rspec-core'	# spec/ requirement
gem 'poltergeist'
