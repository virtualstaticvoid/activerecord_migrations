# activerecord_migrations
Provides a template for Active Record migrations without Rails

# Usage
Instead of defining `RAILS_ENV` you instead define `DATABASE_ENV`. To specify where the migrations live you 
can override the default of `db/migrate` with `MIGRATIONS_DIR`. Just like with rails you provide database 
connection information in `config/database.yml`.

# Rake Tasks
The following rake tasks are available:
 
    rake db:create    # Create the database from config/database.yml for the current DATABASE_ENV
    rake db:drop      # Drops the database for the current DATABASE_ENV
    rake db:migrate   # Migrate the database (options: VERSION=x, VERBOSE=false).
    rake db:rollback  # Rolls the schema back to the previous version (specify steps w/ STEP=n).
    rake db:version   # Retrieves the current schema version number

# Migrations
Create your migrations in the `db/migrate` directory. Like Rails, use a naming convention such as a date 
stamp or sequence number for the file name, followed by the underscored name of the migration class.

E.g.  `001_create_blog_posts_table.rb`

    class CreateBlogPostsTable <  ActiveRecord::Migration
      def up
        create_table :blog_posts do |t|
          t.string :title, :null => false
          t.string :body
          t.boolean :active, :null => false, :default => true
        end
        add_index :blog_posts, :title, :unique => true
      end
     
      def down
        drop_table :blog_posts
      end
    end

# Credits
Taken from Wes Bailey's excellent blog post entitled [ActiveRecord migrations without Rails](http://exposinggotchas.blogspot.com/2011/02/activerecord-migrations-without-rails.html).
