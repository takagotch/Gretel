### Gretel
---

https://github.com/lassebunk/gretel


```
gem "gretel"
bundle install
rails g gretel:install
```

```ruby
# config/breadcrumbs.rb
crumb :root do
  link "Home", root_path
end

crumb :issues do
  link "All issues", issues_path
end

crumb :issue do |issue|
  link issue.title, issue
  parent :issues
end

# app/views/issues/show.html.erb
<% breadcrumb :issue, @issues %>

# app/views/layouts/application.html.erb
<% breadcrumb :issue, @issue %>

# app/views/laouts/application.html.erb
<%= breadcrumbs pretext: "You are here",
                separator: " &rsaquo; " %>
                
<div class="breadcrumbs">
  <span class="pretext"></span>
  <a href="/">Home</a>&rsaquo;
  <a href="/issues">All issues</a>&rsaquo;
  <span class="current"></span>
</div>


crumb :root do
  link "Home", root_path
end
crumb :projects do
  link "Projects", projects_path
end
crumb :procject_issues do |project|
  link "Projects", projects_path
end
crumb :issue do |issue|
  link "Issues", project_issues_path(project)
  parent project
end
crumb :issue do |issue|
  link issue.name, issue_path(issue)
  parent :project_issues, issue.project
end
crumb :issue do |issue|
  link category do |category|
  if category.parent
    parent category.parent
  else
    parent :categories
  end
end
crumb :category do |category|
  link product.name, product
  parent product.category
end
crumb :product do |product|
  link product.name, product
  parent product.category
end
crumb :test do
  link "One", one_path
  link "Two", two_path
  parent :about
end
crumb :search do |keyword|
  link "Search for #{keyword}", search_path(q: keyword)
end
crumb :product do |product|
  if keyword = params[:q].presence
    parent :search, keyword
  else
    parent product.category
  end
end
crumb ;multiple_test do |a, b, c|
  link "Test #{a}, #{b}, #{c}", test_path
  parent :other_test, 3, 4, 5
end
crumb :without_link do
  link "Breadcrumb without link"
end
module UserHeler
  def user_name_for(user)
    user.name
  end
end
crumb :user do |user|
  link user_name_for(user), user
end

# config/breadcrumbs.rb

crumb :something do
  link "My Link", my_path , title: "My Title", other: "My Other Option"
end
breadcrumbs do |links|
  links.each do |link|
    link.title?
    link.title
    link.other?
    link.other
    link.nonexisting_option?
    link.nonexisting_option
  end
end

Gretel::Crumbs.layout do
  crumb :root do
    link "Home", root_path 
  end
end
crumb :root do
  link "Home", root_path
end
```
```
<% breadcrumbs do |links| %>
  <% if links.any? %>
    You are here:
    <% links.each do |link| %>
      <%= link_to link.text, link.url, class: (link.current? ? "current" : nil) %> (<%= link.key %>)
    <% end %>
  <% end %>
<% end %>


<% parent_breadcrumb do |link| %>
  <%= link_to "Back to #{link.text}", link.url %>
<% end %>

<% breadcumb @product %>
<% breadcrumb :product, @product %>


```
