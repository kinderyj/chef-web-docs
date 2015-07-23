## 4. Enable inbound traffic to your web site

On a typical CentOS installation, the [iptables][iptables] service is configured to limit network traffic only to inbound access on port 22 (SSH). In production, you'd likely configure `iptables` to allow explicit inbound and outbound traffic on the ports your services require. But for now, let's take a shortcut and add a second `service` resource to our recipe that stops the `iptables` service. This ensures that inbound traffic on all ports, including port 80 (HTTP), is permitted.

Append a `service` resource to <code class="file-path">webserver.rb</code>, making the complete recipe look like this.

```ruby
# ~/chef-repo/webserver.rb
package 'httpd'

service 'httpd' do
  action [:enable, :start]
end

file '/var/www/html/index.html' do
  content '<html>
  <body>
    <h1>hello world</h1>
  </body>
</html>'
end

service 'iptables' do
  action :stop
end
```
Now apply it.

```bash
# ~/chef-repo/
$ sudo chef-apply webserver.rb
Recipe: (chef-apply cookbook)::(chef-apply recipe)
  * package[httpd] action install (up to date)
  * service[httpd] action enable (up to date)
  * service[httpd] action start (up to date)  
  * file[/var/www/html/index.html] action create (up to date)
  * service[iptables] action stop
    - stop service service[iptables]
```


[iptables]: http://en.wikipedia.org/wiki/Iptables