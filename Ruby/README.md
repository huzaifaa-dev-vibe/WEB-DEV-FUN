# Ruby

> Ruby on Rails: programmer happiness, convention over configuration.

---

## Purpose

Build web apps with Ruby, primarily with Rails.

## Prerequisites

- Programming basics.

## Learning Outcome

You can build, deploy, and scale a Rails app.

## Dependencies

- Ruby 3.2+.

## Related Files

- [Backend/](../Backend/) · [PostgreSQL/](../PostgreSQL/) · [Testing/](../Testing/)

## AI Instructions

When using Ruby/Rails:
1. Use Ruby 3.2+ and Rails 7.1+.
2. Use Active Record (ORM).
3. Use Hotwire (Turbo + Stimulus) for SPA-like UX without JS.
4. Use Sidekiq for background jobs.
5. Use RSpec or Minitest for tests.
6. Use Rubocop for linting.
7. Use Kamal or Heroku for deploy.

## Human Notes

### Install
```bash
# rbenv / mise for version management
gem install rails
rails new myapp
cd myapp && bin/rails server
```

### Structure
```
app/
  models/
  controllers/
  views/
  jobs/
  channels/
config/
  routes.rb
db/
  migrate/
spec/  (or test/)
```

### Model
```ruby
class User < ApplicationRecord
  has_many :posts
  validates :email, presence: true, uniqueness: true
end

User.where(active: true).order(created_at: :desc)
```

### Controller
```ruby
class UsersController < ApplicationController
  def index
    @users = User.includes(:posts).page(params[:page])
  end

  def create
    @user = User.create!(user_params)
    redirect_to @user
  end

  private

  def user_params
    params.require(:user).permit(:name, :email)
  end
end
```

### Routes
```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :users
  root 'users#index'
end
```

### Hotwire (Turbo + Stimulus)
- SPA-like UX without much JS.
- Turbo Drive: page transitions.
- Turbo Frames: partial page updates.
- Turbo Streams: server-driven updates.
- Stimulus: light JS framework.

### Background jobs (Active Job + Sidekiq)
```ruby
class ProcessImageJob < ApplicationJob
  queue_as :default
  def perform(image)
    # ...
  end
end

ProcessImageJob.perform_later(image)
```

### Action Cable (WebSockets)
Built-in.

### Testing (RSpec)
```ruby
RSpec.describe User, type: :model do
  it 'validates email' do
    user = User.new(email: nil)
    expect(user).not_to be_valid
  end
end
```

### Performance
- Ruby 3.x YJIT.
- Puma (multi-threaded server).
- Solid Queue / Sidekiq.
- Cache (Redis).

## Common Mistakes

- ❌ N+1 queries (use `includes`).
- ❌ Fat controllers.
- ❌ Sync work in request cycle.
- ❌ Not using Hotwire (default to JS too often).

## Tools

- Rails docs: https://guides.rubyonrails.org/
- Ruby docs: https://www.ruby-doc.org/
- Rubocop: https://rubocop.org/
- RSpec: https://rspec.info/

## Further Reading

- *The Rails 7 Way* — Obie Fernandez
- *Agile Web Development with Rails* — Sam Ruby et al.
- Hotwire docs: https://hotwired.dev/

## Exercises

1. Build a CRUD app with auth.
2. Add Sidekiq for jobs.
3. Add Hotwire real-time updates.

## Projects

- Build a SaaS with Rails + Stripe + Hotwire.

---

**Previous:** [Laravel/](../Laravel/) · **Next:** [Go/](../Go/) · **Related:** [Backend/](../Backend/)
