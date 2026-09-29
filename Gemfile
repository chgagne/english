source "https://rubygems.org"

# Épinglée : sans contrainte, bundler résout vers une vieille chaîne
# (Jekyll 3.9, Liquid 4.0.3) qui appelle `Object#tainted?`, retiré de Ruby en
# 3.2, et la construction locale échoue. La 232 est celle que GitHub Pages
# exécute, et elle apporte Jekyll 3.10.0 avec Liquid 4.0.4.
gem "github-pages", "~> 232", group: :jekyll_plugins

gem "tzinfo-data"
gem "wdm", "~> 0.1.0" if Gem.win_platform?

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jemoji"
  gem "jekyll-include-cache"
  gem "jekyll-algolia"
  gem "jekyll-redirect-from"
end
