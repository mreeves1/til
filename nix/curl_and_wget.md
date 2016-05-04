# Curl and wget Tips


## Send the hostname in the headers so virtual hosts for instance work
`curl -H 'Host: foo.bar.com' http://127.0.0.1:8080/forums/forum.php`
