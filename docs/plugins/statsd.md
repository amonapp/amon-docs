## StatsD


The Amon agent supports the StatsD protocol, enabling you to easily view custom metrics within Amon.
</br></br>
This eliminates the need to rollout an additional monitoring stack specifically for StatsD (statsd daemon, graphite, alerting, etc) as you can view those metrics on Amon dashboards and create triggers for alerting inside Amon.


### Installation 

The StatsD plugin is preinstalled. To enable it:

<pre><code class="language-bash">$ echo '{"address": ":8125", "delete_timings": true}' > /etc/opt/amonagent/plugins-enabled/statsd.conf
$ sudo service amonagent restart (or) sudo systemctl restart amonagent
</code></pre>

<p>That is it. You can start sending StatsD metrics from your language/platform of choice and you will see them in Amon.</p>

### Supported Metrics

###  Counters

<p>Counters are used to measure the frequency of an event per minute, like page views or failed login attempts. You may specify the amount to increment the counter. </p>

<pre><code class="language-python">import statsd
sc = statsd.StatsClient(port=8125)

sc.incr('amon.counter')
sc.incr('amon.requests')
</code></pre>


### Timers

Timers are used to measure the duration of a task, like database calls or render times.

<pre><code class="language-python">import statsd
sc = statsd.StatsClient(port=8125)

sc.timing('response_timer', 100)
sc.timing('unique_visitors', 300)
</code></pre>>