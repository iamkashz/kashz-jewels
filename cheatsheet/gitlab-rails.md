# gitlab rails

## Recon Gitlab CE using rails

```bash
# find the user:
user = User.find(1)
user = User.find_by(email: "admin@example.com")
user = User.find_by(username: "root")
user = User.find_by(name: "Administrator")
user = User.find_by(admin: true)

# pretty_print parameters
pp u.attributes

# change the password
user.password = 'kashz'
user.password_confirmation = 'kashz'

# and save
user.save
```

{% embed url="https://gist.github.com/dnozay/188f256839d4739ca3e4" %}
