The amonagent is a single golang binary. There is nothing to install and all dependencies are already bundled in.
To enable a plugin, the only thing you have to do is edit the configuration file in <code class="language-bash">/etc/opt/amonagent/plugins-enabled/{plugin}.conf</code> and restart the agent

<ol>
    <li>To list all available plugins run <code class="language-bash">/opt/amonagent/amonagent -list-plugins</code></li>
    <li>To test a plugin run <code class="language-bash">/opt/amonagent/amonagent -test-plugin={name}</code></li>
    <li>To display all available configuration option for a plugin run <code class="language-bash">/opt/amonagent/amonagent -plugin-config={name}</code></li>
</ol>

## StatsD

<p>


The Amon agent supports the StatsD protocol, enabling you to easily view custom metrics within Amon.
<br><br>
This eliminates the need to rollout an additional monitoring stack specifically for StatsD (statsd daemon, graphite, alerting, etc) as you can view those metrics on Amon dashboards and create triggers for alerting inside Amon.



</p>


<h3>Installation</h3>
<p>The StatsD is preinstalled. To enable it: </p>

<pre class='codehighlight'><code class="language-bash">$ echo '{"address": ":8125", "delete_timings": true}' > /etc/opt/amonagent/plugins-enabled/statsd.conf
$ sudo service amonagent restart (or) sudo systemctl restart amonagent</code></pre>

<p>That is it. You can start sending StatsD metrics from your language/platform of choice and you will see them in Amon.</p>

<h3>Supported Metrics</h3>
<h4>Counters</h4>
<p>Counters are used to measure the frequency of an event per minute, like page views or failed login attempts. You may specify the amount to increment the counter. </p>


<pre><code class="language-python">import statsd
sc = statsd.StatsClient(port=8125)

sc.incr('amon.counter')
sc.incr('amon.requests')
</code></pre>


<h4>Timers</h4>
<p>Timers are used to measure the duration of a task, like database calls or render times.</p>

<pre><code class="language-python">import statsd
sc = statsd.StatsClient(port=8125)

sc.timing('response_timer', 100)
sc.timing('unique_visitors', 300)
</code></pre>


## Health Checks

## Sensu

## Telegraf

## Custom