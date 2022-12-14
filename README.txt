# ntfy_config
Some config to ntfy app!

curl \
    -u phil:mypass \
    -d "Look ma, with auth" \
    http://ntfy.example.com/mysecrets
    
Commands:

ntfy user list                     # Shows list of users (alias: 'ntfy access')
ntfy user add phil                 # Add regular user phil  
ntfy user add --role=admin phil    # Add admin user phil
ntfy user del phil                 # Delete user phil
ntfy user change-pass phil         # Change password for user phil
ntfy user change-role phil admin   # Make user phil an admin

ntfy access                            # Shows access control list (alias: 'ntfy user list')
ntfy access USERNAME                   # Shows access control entries for USERNAME
ntfy access USERNAME TOPIC PERMISSION  # Allow/deny access for USERNAME to TOPIC

read-write (alias: rw): Allows publishing messages to the given topic, as well as subscribing and reading messages
read-only (aliases: read, ro): Allows only subscribing and reading messages, but not publishing to the topic
write-only (aliases: write, wo): Allows only publishing to the topic, but not subscribing to it
deny (alias: none): Allows neither publishing nor subscribing to a topic

ntfy access                        # Shows entire access control list
ntfy access phil                   # Shows access for user phil
ntfy access phil mytopic rw        # Allow read-write access to mytopic for user phil
ntfy access everyone mytopic rw    # Allow anonymous read-write access to mytopic
ntfy access everyone "up*" write   # Allow anonymous write-only access to topics "up..."
ntfy access --reset                # Reset entire access control list
ntfy access --reset phil           # Reset all access for user phil
ntfy access --reset phil mytopic   # Reset access for user phil and topic mytopic

ntfy access:

user phil (admin)
- read-write access to all topics (admin role)
user ben (user)
- read-write access to topic garagedoor
- read-write access to topic alerts*
- read-only access to topic furnace
user * (anonymous)
- read-only access to topic announcements
- read-only access to topic server-stats
- no access to any (other) topics (server config)
