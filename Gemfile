source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins

    # gem "jekyll", ">= 3.5", "< 5.0"
    group :jekyll_plugins do
      gem "jekyll-sitemap", "~> 1.2.0"
      gem "jekyll-feed", "~> 0.11.0" 
      gem "jekyll-seo-tag", "~> 2.5.0"
      gem "jekyll-paginate", "~> 1.1.0"
      gem "jekyll-gist", "~> 1.5.0"
    end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.0", :install_if => Gem.win_platform?

