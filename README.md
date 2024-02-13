# README

**Live on https://mysite-zccj.onrender.com/

**TODO
- adding :confirmable to user model and fix resend smtp service (timing out)

- `rails new . --css tailwind`
- Added font-awesome and devise manually in Gemfile, bundle install
- bin/rails g devise:install
- rails g scaffold Course title:string description:string
- bin/rails g devise User
- bin/rails g devise Admin
- bin/rails db:migrate
- rails c -> Admin.create(email...)
- After installing libvips and FFmpeg, uncomment image_processing gem && bin/rails active_storage:install
- rails db:migrate
- now that active_storage setup, add it to modal
- c = Course.first, c.image, c.image.present, c.image.attach(io: File.open("#{Rails.root}/app/assets/images/colorful4.jpg"), filename: "rails-ecomm.png") DOUBLE QUOTATION... beautiful... same with Course.second...
- bin/rails g scaffold Lesson title:string description:text paid:boolean course:references
- <%=> displays content, for if statement no equals (<% %>)
- Adding video: c = Course.find 1, c.lessons.create!(title: "Lesson 1", description: "Lesson 1"), l = c.lessons.first, l.video.attach(io: File.open("#{Rails.root}/app/assets/videos/The STD Song.mp4"), filename: "The STD Song.mp4")
- bin/rails g model Category name:string
- rails db:migrate
- rails c, Category.create!(name: "Rails 7")... repeat for as many technoligies
- create joins table: bin/rails g migration create_categories_courses... adding col manually in create_categories_courses.rb
- db:migrate (create tables)
- add to models has_many_and_belongs_to...
- rails c (associate categories with course): c = Course.find 1, cat1 = Category.first, c.categories.push(cat1), c.save!, c.reload, c.categories, cat2 = Category.last, c.categories.push(cat2), c.categories.destroy_all (had duplicate since error of doing cat1 again), c.categories (empty now), repeat and how have id 1 and 5, Rails 7 and Stripe c.categories.
- Another lesson for plural: rails c, c = Course.find 1, c.lessons.create(title: "Lesson 2", description: "Lesson 2"), l = Lesson.last, l.video.attach(io: File.open("#{Rails.root}/app/assets/videos/..."), filename: "...")
- bin/rails g migration add_more_cols_to_course, add cols manually in migrate file (to update table), db:migrate, see schema (cols are added) ---> @course.paid would've thrown error until added that col to migrate and migrated the change to schema
- :confirmable to user model for email confirm
- bin/rails g migration add_confirmable_to_user, add columns, db:migrate
- now sign up as user, email has been sent, can see the email in the terminal (scroll up) ---> copy the href for confirmation token, visit url and that will confirm email
- bin/rails g migration add_position_to_lessons ---> now can use :position in course.rb since now a column
- course_lesson path (got to /roueosu and search), doesn't exist, needed lessons resource to be nested in courses
- don't want users to creat/patch/destroy lessons (delete code in those methods, change with change bool to true watched)
- hamburger menu: stimulus controller -> bin/rails g stimulus navbar
- bin/rails g devise:views -> moves all nested devise views to accessable (able customize sign_in type pages)
- bin/rails g model LessonUser lesson:references user:references completed:boolean
- next lesson: issues because :position was nil (c = Course.find 1, c.lessons): l1 = c.lessons.first, l1.position = 1, l1.save, l2 = c.lessons.last, l2.position = 2, l2.save, c.lessons -> positions defined
- after updating and things: add lesson to course as test -> c = Course.find 1, Lesson.create!(...id 1) -> forgot position so it's at top
- rails c, c = Course.find 1, ls = c.lessons, l = ls.last, l.position = 3, l.save
- bin/rails g controller checkouts
- VISUAL=vim bin/rails credentials:edit (set secrets)
- Course.all.each do |c| c.update_attribute(:paid, true); end
- c = Course.find 1, c.stripe_price_id => nil, ---> go to stripe and create product, c.stripe_price_id = "price...", c.save!
- bin/rails g controller webhooks_controller
- VISUAL=vim bin/rails credentials:edit
- bin/rails g model CourseUser course:references user:references
- db:migrate
- make stripe webhook endpoint listening purchase, rails c, c = Course.find 1, c.course_users --> will see 1 purchased user
- rails c, c = Course.find 1, c.lessons.create!(...), l = Lesson.last, l.paid = true. l.save!
- bin/rails g controller Admin::Courses
- bin/rails g erb:scaffold Admin::Course
- bin/rails g controller Admin::Lessons
- bin/rails g erb:scaffold Admin::Lessons
- bin/importmap pin stimulus-sortable
- bin/importmap pin sortable.js
- bin/importmap pin @rails/request.js
- bin/importmap pin chart.js
- bin/rails g stimulus dashboard
- fix chartjs issue: 1. "importmap-rails", "1.2.3",, "stimulus-rails", "1.3.0"... 2. bin/importmap unpin chart.js... 3. bin/importmap pin chart.js
- bin/rails g controller Admin::Users
- bin/rails g erb:scaffold Admin::Users

*Deploy
- docs.render.com/deploy-rails (skip to step 3)
- do swap to postgresql
- VISUAL=vim bin/rails credentials:edit (add aws keys)

*Render issue
- add db:migrate -> to render-build.sh

*Create admin seed with free render
- add db:seed to render-build.sh
- add below to seeds
```
# Create a default admin user
if !Admin.exists?(email: "Jane@doe.com")
  Admin.create!(email: "Jane@doe.com", password: "asjkfdgh234975")
end
```