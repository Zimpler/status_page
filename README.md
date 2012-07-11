Status Page
===========

A very simple gem for displaying a status page with configurable
status checks

How to use
----------

{% highlight ruby %}

# app/models/my_status.rb
class MyStatus < StatusPage::Status
  def check
    if some_error_condition
      @errors << "I've made a huge mistake"
    end
    if some_warning_condition
      @warnings << "I've made a small mistake"
    end
  end
end

# config/initializers/status_page.rb
StatusPage.checks += [
  "StatusPage::ActiveRecordStatus",    # checks database connection
  "MyStatus"
]

# config/routes.rb
#
# Route /status to StatusPage::MainController#index

scope :module => :status_page do
  get "/status" => "main#index"
end

{% endhighlight %}
