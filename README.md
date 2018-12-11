# Python_FlaskApp1
This app is created based on the following article:
https://code.visualstudio.com/docs/python/tutorial-flask

<h1>Use Flask in Visual Studio Code</h1>
<p><a href="http://flask.pocoo.org/" class="external-link" target="_blank">Flask</a> is a lightweight Python framework for web applications that provides the basics for URL routing and page rendering.</p>
<p>Flask is called a &quot;micro&quot; framework because it doesn't directly provide features like form validation, database abstraction, authentication, and so on. Such features are instead provided by special Python packages called Flask <a href="http://flask.pocoo.org/extensions/" class="external-link" target="_blank">extensions</a>. The extensions integrate seamlessly with Flask so that they appear as if they were part of Flask itself. For example, Flask doesn't provide a page template engine, but installing Flask includes the <a href="http://jinja.pocoo.org/" class="external-link" target="_blank">Jinja</a> templating engine by default. For convenience, we typically speak of these defaults as part of Flask.</p>
<p>In this tutorial you create a simple Flask app with three pages that use a common base template. Along the way you experience a number of features of Visual Studio Code including using the terminal, the editor, the debugger, code snippets, and more.</p>
<p>The completed code project from this tutorial can be found on GitHub: <a href="https://github.com/Microsoft/python-sample-vscode-flask-tutorial" class="external-link" target="_blank">python-sample-vscode-flask-tutorial</a>.</p>
<p>If you have any problems, feel free to file an issue for this tutorial in the <a href="https://github.com/Microsoft/vscode-docs/issues" class="external-link" target="_blank">VS Code documentation repository</a>.</p>
<h2 id="_prerequisites" data-needslink="_prerequisites">Prerequisites</h2>
<p>To successfully complete this tutorial, you must do the following (which are the same steps as in the <a href="/docs/python/python-tutorial">general Python tutorial</a>):</p>
<ol>
<li>
<p>Install the <a href="https://marketplace.visualstudio.com/items?itemName=ms-python.python" class="external-link" target="_blank">Python extension</a>.</p>
</li>
<li>
<p>Install a version of Python 3 (for which this tutorial is written). Options include:</p>
<ul>
<li>(All operating systems) A download from <a href="https://www.python.org/downloads/" class="external-link" target="_blank">python.org</a>; typically use the <strong>Download Python 3.6.5</strong> button that appears first on the page (or whatever is the latest version).</li>
<li>(Linux) The built-in Python 3 installation works well, but to install other Python packages you must run <code>sudo apt install python3-pip</code> in the terminal.</li>
<li>(macOS) An installation through <a href="https://brew.sh/" class="external-link" target="_blank">Homebrew</a> on macOS using <code>brew install python3</code> (the system install of Python on macOS is not supported).</li>
<li>(All operating systems) A download from <a href="https://www.anaconda.com/download/" class="external-link" target="_blank">Anaconda</a> (for data science purposes).</li>
</ul>
</li>
<li>
<p>On Windows, make sure the location of your Python interpreter is included in your PATH environment variable. You can check this by running <code>path</code> at the command prompt. If the Python interpreter's folder isn't included, open Windows Settings, search for &quot;environment&quot;, select <strong>Edit environment variables for your account</strong>, then edit the <strong>Path</strong> variable to include that folder.</p>
</li>
</ol>
<h2 id="_create-a-project-environment-for-flask" data-needslink="_create-a-project-environment-for-flask">Create a project environment for Flask</h2>
<p>In this section you create a virtual environment in which Flask is installed. Using a virtual environment avoids installing Flask into a global Python environment and gives you exact control over the libraries used in an application. A virtual environment also makes it easy to <a href="#_create-a-requirementstxt-file-for-the-environment">Create a requirements.txt file for the environment</a>.</p>
<ol>
<li>
<p>On your file system, create a project folder for this tutorial, such as <code>hello_flask</code>.</p>
</li>
<li>
<p>In that folder, use the following command (as appropriate to your computer) to create a virtual environment named <code>env</code> based on your current interpreter:</p>
<pre><code class="bash"><span class="hljs-comment"># macOS/Linux</span>
sudo apt-get install python3-venv    <span class="hljs-comment"># If needed</span>
python3 -m venv env

<span class="hljs-comment"># Windows</span>
python -m venv env
</code></pre>
<blockquote>
<p><strong>Note</strong>: Use a stock Python installation when running the above commands. If you use <code>python.exe</code> from an Anaconda installation, you see an error because the ensurepip module isn't available, and the environment is left in an unfinished state.</p>
</blockquote>
</li>
<li>
<p>Open the project folder in VS Code by running <code>code .</code>, or by running VS Code and using the <strong>File</strong> &gt; <strong>Open Folder</strong> command.</p>
</li>
<li>
<p>In VS Code, open the Command Palette (<strong>View</strong> &gt; <strong>Command Palette</strong> or (<span class="dynamic-keybinding" data-osx="⇧⌘P" data-win="Ctrl+Shift+P" data-linux="Ctrl+Shift+P"><span class="keybinding">⇧⌘P</span> (Windows, Linux <span class="keybinding">Ctrl+Shift+P</span>)</span>)). Then select the <strong>Python: Select Interpreter</strong> command:</p>
<p><img src="/assets/docs/python/shared/command-palette.png" alt="Opening the Command Palette in VS Code"></p>
</li>
<li>
<p>The command presents a list of available interpreters that VS Code can locate automatically (your list will vary; if you don't see the desired interpreter, see <a href="/docs/python/environments">Configuring Python environments</a>). From the list, select the virtual environment in your project folder that starts with <code>./env</code> or <code>.\env</code>:</p>
<p><img src="/assets/docs/python/shared/select-virtual-environment.png" alt="Selecting the virtual environment for Python"></p>
</li>
<li>
<p>Run <strong>Terminal: Create New Integrated Terminal</strong> (<span class="dynamic-keybinding" data-osx="⌃⇧`" data-win="Ctrl+Shift+`" data-linux="Ctrl+Shift+`"><span class="keybinding">⌃⇧`</span> (Windows, Linux <span class="keybinding">Ctrl+Shift+`</span>)</span>)) from the Command Palette, which creates a terminal and automatically activates the virtual environment by running its activation script.</p>
<blockquote>
<p><strong>Note</strong>: On Windows, if your default terminal type is PowerShell, you may see an error that it cannot run activate.ps1 because running scripts is disabled on the system. The error provides a link for information on how to allow scripts. Otherwise, use <strong>Terminal: Select Default Shell</strong> to set &quot;Command Prompt&quot; or &quot;Git Bash&quot; as your default instead.</p>
</blockquote>
</li>
<li>
<p>The selected environment appears on the left side of the VS Code status bar, and notice the &quot;(venv)&quot; indicator that tells you that you're using a virtual environment:</p>
<p><img src="/assets/docs/python/shared/environment-in-status-bar.png" alt="Selected environment showing in the VS Code status bar"></p>
</li>
<li>
<p>Install Flask in the virtual environment by running one of the following commands in the VS Code Terminal:</p>
<pre><code class="bash"><span class="hljs-comment"># macOS/Linux</span>
pip3 install flask

<span class="hljs-comment"># Windows</span>
pip install flask
</code></pre>
</li>
</ol>
<p>You now have a self-contained environment ready for writing Flask code. VS Code activates the environment automatically when you use <strong>Terminal: Create New Integrated Terminal</strong>. If you open a separate command prompt or terminal, activate the environment by running <code>source env/bin/activate</code> (Linux/macOS) or <code>env\scripts\activate</code> (Windows).  You know the environment is activated when the command prompt shows <strong>(env)</strong> at the beginning.</p>
<h2 id="_create-and-run-a-minimal-flask-app" data-needslink="_create-and-run-a-minimal-flask-app">Create and run a minimal Flask app</h2>
<ol>
<li>
<p>In VS Code, create a new file in your project folder named <code>app.py</code> using either <strong>File</strong> &gt; <strong>New</strong> from the menu, pressing <span class="keybinding">Ctrl+N</span>, or using the new file icon in the Explorer View (shown below).</p>
<p><img src="/assets/docs/python/flask/new-file-icon.png" alt="New file icon in Explorer View"></p>
</li>
<li>
<p>In <code>app.py</code>, add code to import Flask and create an instance of the Flask object. If you type the code below (instead of using copy-paste), you can observe VS Code's <a href="/docs/python/editing#_autocomplete-and-intellisense">IntelliSense and auto-completions</a>:</p>
<pre><code class="python"><span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> Flask
app = Flask(__name__)
</code></pre>
</li>
<li>
<p>Also in <code>app.py</code>, add a function that returns content, in this case a simple string, and use Flask's <code>app.route</code> decorator to map the URL route <code>/</code> to that function:</p>
<pre><code class="python"><span class="hljs-decorator">@app.route("/")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">home</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> <span class="hljs-string">"Hello, Flask!"</span>
</code></pre>
<blockquote>
<p><strong>Tip</strong>: You can use multiple decorators on the same function, one per line, depending on how many different routes you want to map to the same function.</p>
</blockquote>
</li>
<li>
<p>Save the <code>app.py</code> file (<span class="dynamic-keybinding" data-osx="⌘S" data-win="Ctrl+S" data-linux="Ctrl+S"><span class="keybinding">⌘S</span> (Windows, Linux <span class="keybinding">Ctrl+S</span>)</span>).</p>
</li>
<li>
<p>In the terminal, run the app by entering <code>python3 -m flask run</code> (macOS/Linux) or <code>python -m flask run</code> (Windows), which runs the Flask development server. The development server looks for <code>app.py</code> by default. When you run Flask, you should see output similar to the following:</p>
<pre><code class="bash">(env) D:\py\\hello_flask&gt;python -m flask run
 * Environment: production
   WARNING: Do not use the development server <span class="hljs-keyword">in</span> a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://<span class="hljs-number">127.0</span>.<span class="hljs-number">0.1</span>:<span class="hljs-number">5000</span>/ (Press CTRL+C to quit)
</code></pre>
<p>If you see an error that the Flask module cannot be found, make sure you've run <code>pip3 install flask</code> (macOS/Linux) or <code>pip install flask</code> (Windows) in your virtual environment as described at the end of the previous section.</p>
<p>Also, if you want to run the development server on a different IP address or port, use the host and port command line arguments, as with <code>--host=0.0.0.0 --port=80</code>.</p>
</li>
<li>
<p>To open your default browser to the rendered page, <span class="keybinding">Ctrl+click</span> the <code>http://127.0.0.1:5000/</code> URL in the terminal.</p>
<p><img src="/assets/docs/python/flask/app-in-browser-01.png" alt="The running app in a browser"></p>
</li>
<li>
<p>Observe that when you visit a URL like /, a message appears in the debug terminal showing the HTTP request:</p>
<pre><code class="bash"><span class="hljs-number">127.0</span>.<span class="hljs-number">0.1</span> - - [<span class="hljs-number">11</span>/Jul/<span class="hljs-number">2018</span> <span class="hljs-number">08</span>:<span class="hljs-number">40</span>:<span class="hljs-number">15</span>] <span class="hljs-string">"GET / HTTP/1.1"</span> <span class="hljs-number">200</span> -
</code></pre>
</li>
<li>
<p>Stop the app by using <span class="keybinding">Ctrl+C</span> in the terminal.</p>
</li>
</ol>
<blockquote>
<p><strong>Tip</strong>: If you want to use a different filename than <code>app.py</code>, such as <code>program.py</code>, define an environment variable named FLASK_APP and set its value to your chosen file. Flask's development server then uses the value of FLASK_APP instead of the default file <code>app.py</code>. For more information, see <a href="http://flask.pocoo.org/docs/1.0/cli/" class="external-link" target="_blank">Flask command line interface</a>.</p>
</blockquote>
<h2 id="_run-the-app-in-the-debugger" data-needslink="_run-the-app-in-the-debugger">Run the app in the debugger</h2>
<p>Debugging gives you the opportunity to pause a running program on a particular line of code. When a program is paused, you can examine variables, run code in the Debug Console panel, and otherwise take advantage of the features described on <a href="/docs/python/debugging">Debugging</a>. Running the debugger also automatically saves any modified files before the debugging session begins.</p>
<p><strong>Before you begin</strong>: Make sure you've stopped the running app at the end of the last section by using <span class="keybinding">Ctrl+C</span> in the terminal. If you leave the app running in one terminal, it continues to own the port. As a result, when you run the app in the debugger using the same port, the original running app handles all the requests and you won't see any activity in the app being debugged and the program won't stop at breakpoints. In other words, if the debugger doesn't seem to be working, make sure that no other instance of the app is still running.</p>
<ol>
<li>
<p>Replace the contents of <code>app.py</code> with the following code, which adds a second route and function that you can step through in the debugger:</p>
<pre><code class="python"><span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> Flask
<span class="hljs-keyword">from</span> datetime <span class="hljs-keyword">import</span> datetime
<span class="hljs-keyword">import</span> re

app = Flask(__name__)

<span class="hljs-decorator">@app.route("/")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">home</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> <span class="hljs-string">"Hello, Flask!"</span>

<span class="hljs-decorator">@app.route("/hello/&lt;name&gt;")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">hello_there</span><span class="hljs-params">(name)</span>:</span>
    now = datetime.now()
    formatted_now = now.strftime(<span class="hljs-string">"%A, %d %B, %Y at %X"</span>)

    <span class="hljs-comment"># Filter the name argument to letters only using regular expressions. URL arguments</span>
    <span class="hljs-comment"># can contain arbitrary text, so we restrict to safe characters only.</span>
    match_object = re.match(<span class="hljs-string">"[a-zA-Z]+"</span>, name)

    <span class="hljs-keyword">if</span> match_object:
        clean_name = match_object.group(<span class="hljs-number">0</span>)
    <span class="hljs-keyword">else</span>:
        clean_name = <span class="hljs-string">"Friend"</span>

    content = <span class="hljs-string">"Hello there, "</span> + clean_name + <span class="hljs-string">"! It's "</span> + formatted_now
    <span class="hljs-keyword">return</span> content
</code></pre>
<p>The decorator used for the new URL route, <code>/hello/&lt;name&gt;</code>, defines an endpoint /hello/ that can accept any additional value. The identifier inside <code>&lt;</code> and <code>&gt;</code> in the route defines a variable that is passed to the function and can be used in your code.</p>
<p>URL routes are case-sensitive. For example, the route <code>/hello/&lt;name&gt;</code> is distinct from <code>/Hello/&lt;name&gt;</code>. If you want the same function to handle both, use decorators for each variant.</p>
<p>As described in the code comments, always filter arbitrary user-provided information to avoid various attacks on your app. In this case, the code filters the name argument to contain only letters, which avoids injection of control characters, HTML, and so forth. (When you use templates in the next section, Flask does automatic filtering and you won't need this code.)</p>
</li>
<li>
<p>Set a breakpoint at the first line of code in the <code>hello_there</code> function (<code>now = datetime.now()</code>) by doing any one of the following:</p>
<ul>
<li>With the cursor on that line, press <span class="dynamic-keybinding" data-osx="F9" data-win="F9" data-linux="F9"><span class="keybinding">F9</span></span>, or,</li>
<li>With the cursor on that line, select the <strong>Debug</strong> &gt; <strong>Toggle Breakpoint</strong> menu command, or,</li>
<li>Click directly in the margin to the left of the line number (a faded red dot appears when hovering there).</li>
</ul>
<p>The breakpoint appears as a red dot in the left margin:</p>
<p><img src="/assets/docs/python/flask/debug-breakpoint-set.png" alt="A breakpoint set on the first line of the hello_there function"></p>
</li>
<li>
<p>Switch to <strong>Debug</strong> view in VS Code (using the left-side activity bar). Along the top of the Debug view, you may see &quot;No Configurations&quot; and a warning dot on the gear icon. Both indicators mean that you don't yet have a <code>launch.json</code> file containing debug configurations:</p>
<p><img src="/assets/docs/python/shared/debug-panel-initial-view.png" alt="Initial view of the debug panel"></p>
</li>
<li>
<p>Select the gear icon and select <strong>Python</strong> from the list that appears. VS Code creates and opens a <code>launch.json</code> file. This JSON file contains a number of debugging configurations, each of which is a separate JSON object within the <code>configuration</code> array.</p>
</li>
<li>
<p>Scroll down to and examine the configuration with the name &quot;Python: Flask (0.11.x or later)&quot;. This configuration contains <code>&quot;module&quot;: &quot;flask&quot;,</code>, which tells VS Code to run Python with <code>-m flask</code> when it starts the debugger. It also defines the FLASK_APP environment variable in the <code>env</code> property to identify the startup file, which is <code>app.py</code> by default, but allows you to easily specify a different file. If you want to change the host and/or port, you can use the <code>args</code> array.</p>
<pre><code class="json">{
    "<span class="hljs-attribute">name</span>": <span class="hljs-value"><span class="hljs-string">"Python: Flask (0.11.x or later)"</span></span>,
    "<span class="hljs-attribute">type</span>": <span class="hljs-value"><span class="hljs-string">"python"</span></span>,
    "<span class="hljs-attribute">request</span>": <span class="hljs-value"><span class="hljs-string">"launch"</span></span>,
    "<span class="hljs-attribute">module</span>": <span class="hljs-value"><span class="hljs-string">"flask"</span></span>,
    "<span class="hljs-attribute">env</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">FLASK_APP</span>": <span class="hljs-value"><span class="hljs-string">"app.py"</span>
    </span>}</span>,
    "<span class="hljs-attribute">args</span>": <span class="hljs-value">[
        <span class="hljs-string">"run"</span>,
        <span class="hljs-string">"--no-debugger"</span>,
        <span class="hljs-string">"--no-reload"</span>
    ]
</span>},
</code></pre>
<blockquote>
<p><strong>Note</strong>: If the <code>env</code> entry in your configuration contains <code>&quot;FLASK_APP&quot;: &quot;${workspaceFolder}/app.py&quot;</code>, change it to <code>&quot;FLASK_APP&quot;: &quot;app.py&quot;</code> as shown above. Otherwise you may encounter error messages like &quot;Cannot import module C&quot; where C is the drive letter where your project folder resides.</p>
</blockquote>
</li>
<li>
<p>Save <code>launch.json</code> (<span class="dynamic-keybinding" data-osx="⌘S" data-win="Ctrl+S" data-linux="Ctrl+S"><span class="keybinding">⌘S</span> (Windows, Linux <span class="keybinding">Ctrl+S</span>)</span>). In the debug configuration drop-down list (which reads <strong>Python: Current File</strong>) select the <strong>Python: Flask (0.11.x or later)</strong> configuration .</p>
<p><img src="/assets/docs/python/flask/debug-select-configuration.png" alt="Selecting the Flask debugging configuration"></p>
</li>
<li>
<p>Start the debugger by selecting the <strong>Debug</strong> &gt; <strong>Start Debugging</strong> menu command, or selecting the green <strong>Start Debugging</strong> arrow next to the list (<span class="dynamic-keybinding" data-osx="F5" data-win="F5" data-linux="F5"><span class="keybinding">F5</span></span>):</p>
<p><img src="/assets/docs/python/flask/debug-continue-arrow.png" alt="Start debugging/continue arrow on the debug toolbar"></p>
<p>Observe that the status bar changes color to indicate debugging:</p>
<p><img src="/assets/docs/python/flask/debug-status-bar.png" alt="Appearance of the debugging status bar"></p>
<p>A debugging toolbar (shown below) also appears in VS Code containing commands in the following order: Pause (or Continue, <span class="dynamic-keybinding" data-osx="F5" data-win="F5" data-linux="F5"><span class="keybinding">F5</span></span>), Step Over (<span class="dynamic-keybinding" data-osx="F10" data-win="F10" data-linux="F10"><span class="keybinding">F10</span></span>), Step Into (<span class="dynamic-keybinding" data-osx="F11" data-win="F11" data-linux="F11"><span class="keybinding">F11</span></span>), Step Out (<span class="dynamic-keybinding" data-osx="⇧F11" data-win="Shift+F11" data-linux="Shift+F11"><span class="keybinding">⇧F11</span> (Windows, Linux <span class="keybinding">Shift+F11</span>)</span>), Restart (<span class="dynamic-keybinding" data-osx="⇧⌘F5" data-win="Ctrl+Shift+F5" data-linux="Ctrl+Shift+F5"><span class="keybinding">⇧⌘F5</span> (Windows, Linux <span class="keybinding">Ctrl+Shift+F5</span>)</span>), and Stop (<span class="dynamic-keybinding" data-osx="⇧F5" data-win="Shift+F5" data-linux="Shift+F5"><span class="keybinding">⇧F5</span> (Windows, Linux <span class="keybinding">Shift+F5</span>)</span>). See <a href="/docs/editor/debugging">VS Code debugging</a> for a description of each command.</p>
<p><img src="/assets/docs/python/flask/debug-toolbar.png" alt="The VS Code debug toolbar"></p>
</li>
<li>
<p>Output appears in a &quot;Python Debug Console&quot; terminal. <span class="keybinding">Ctrl+click</span> the <code>http://127.0.0.1:5000/</code> link in that terminal to open a browser to that URL. In the browser's address bar, navigate to <code>http://127.0.0.1:5000/hello/VSCode</code>. Before the page renders, VS Code pauses the program at the breakpoint you set. The small yellow arrow on the breakpoint indicates that it's the next line of code to run.</p>
<p><img src="/assets/docs/python/flask/debug-program-paused.png" alt="VS Code paused at a breakpoint"></p>
</li>
<li>
<p>Use Step Over to run the <code>now = datetime.now()</code> statement.</p>
</li>
<li>
<p>On the left side of the VS Code window you see a <strong>Variables</strong> pane that shows local variables, such as <code>now</code>, as well as arguments, such as <code>name</code>. Below that are panes for <strong>Watch</strong>, <strong>Call Stack</strong>, and <strong>Breakpoints</strong> (see <a href="/docs/editor/debugging">VS Code debugging</a> for details). In the <strong>Locals</strong> section, try expanding different values. You can also double-click values (or use <span class="dynamic-keybinding" data-osx="Enter" data-win="F2" data-linux="F2"><span class="keybinding">Enter</span> (Windows, Linux <span class="keybinding">F2</span>)</span>) to modify them. Changing variables such as <code>now</code>, however, can break the program. Developers typically make changes only to correct values when the code didn't produce the right value to begin with.</p>
<p><img src="/assets/docs/python/flask/debug-local-variables.png" alt="Local variables and arguments in VS Code during debugging"></p>
</li>
<li>
<p>When a program is paused, the <strong>Debug Console</strong> panel (which is different from the &quot;Python Debug Console&quot; in the Terminal panel) lets you experiment with expressions and try out bits of code using the current state of the program. For example, once you've stepped over the line <code>now = datetime.now()</code>, you might experiment with different date/time formats. In the editor, select the code that reads <code>now.strftime(&quot;%A, %d %B, %Y at %X&quot;)</code>, then right-click and select <strong>Debug: Evaluate</strong> to send that code to the debug console, where it runs:</p>
<pre><code class="bash">now.strftime(<span class="hljs-string">"%A, %d %B, %Y at %X"</span>)
<span class="hljs-string">'Wednesday, 31 October, 2018 at 18:13:39'</span>
</code></pre>
<blockquote>
<p><strong>Tip</strong>: The <strong>Debug Console</strong> also shows exceptions from within the app that may not appear in the terminal. For example, if you see a &quot;Paused on exception&quot; message in the <strong>Call Stack</strong> area of Debug View, switch to the <strong>Debug Console</strong> to see the exception message.</p>
</blockquote>
</li>
<li>
<p>Copy that line into the &gt; prompt at the bottom of the debug console, and try changing the formatting:</p>
<pre><code class="bash">now.strftime(<span class="hljs-string">"%a, %d %B, %Y at %X"</span>)
<span class="hljs-string">'Wed, 31 October, 2018 at 18:13:39'</span>
now.strftime(<span class="hljs-string">"%a, %d %b, %Y at %X"</span>)
<span class="hljs-string">'Wed, 31 Oct, 2018 at 18:13:39'</span>
now.strftime(<span class="hljs-string">"%a, %d %b, %y at %X"</span>)
<span class="hljs-string">'Wed, 31 Oct, 18 at 18:13:39'</span>
</code></pre>
<blockquote>
<p><strong>Note</strong>: If you see a change you like, you can copy and paste it into the editor during a debugging session. However, those changes aren't applied until you restart the debugger.</p>
</blockquote>
</li>
<li>
<p>Step through a few more lines of code, if you'd like, then select Continue (<span class="dynamic-keybinding" data-osx="F5" data-win="F5" data-linux="F5"><span class="keybinding">F5</span></span>) to let the program run. The browser window shows the result:</p>
<p><img src="/assets/docs/python/flask/debug-run-result.png" alt="Result of the modified program"></p>
</li>
<li>
<p>Close the browser and stop the debugger when you're finished. To stop the debugger, use the Stop toolbar button (the red square) or the <strong>Debug</strong> &gt; <strong>Stop Debugging</strong> command (<span class="dynamic-keybinding" data-osx="⇧F5" data-win="Shift+F5" data-linux="Shift+F5"><span class="keybinding">⇧F5</span> (Windows, Linux <span class="keybinding">Shift+F5</span>)</span>).</p>
</li>
</ol>
<blockquote>
<p><strong>Tip</strong>: To make it easier to repeatedly navigate to a specific URL like <code>http://127.0.0.1:5000/hello/VSCode</code>, output that URL using a <code>print</code> statement. The URL appears in the terminal where you can use <span class="keybinding">Ctrl+click</span> to open it in a browser.</p>
</blockquote>
<h2 id="_go-to-definition-and-peek-definition-commands" data-needslink="_go-to-definition-and-peek-definition-commands">Go to Definition and Peek Definition commands</h2>
<p>During your work with Flask or any other library, you may want to examine the code in those libraries themselves. VS Code provides two convenient commands that navigate directly to the definitions of classes and other objects in any code:</p>
<ul>
<li>
<p><strong>Go to Definition</strong> jumps from your code into the code that defines an object. For example, in <code>app.py</code>, right-click on the <code>Flask</code> class (in the line <code>app = Flask(__name__)</code>) and select <strong>Go to Definition</strong> (or use <span class="dynamic-keybinding" data-osx="F12" data-win="F12" data-linux="F12"><span class="keybinding">F12</span></span>), which navigates to the class definition in the Flask library.</p>
</li>
<li>
<p><strong>Peek Definition</strong> (<span class="dynamic-keybinding" data-osx="⌥F12" data-win="Alt+F12" data-linux="Ctrl+Shift+F10"><span class="keybinding">⌥F12</span> (Windows <span class="keybinding">Alt+F12</span>, Linux <span class="keybinding">Ctrl+Shift+F10</span>)</span>, also on the right-click context menu), is similar, but displays the class definition directly in the editor (making space in the editor window to avoid obscuring any code). Press <span class="keybinding">Escape</span> to close the Peek window or use the <strong>x</strong> in the upper right corner.</p>
<p><img src="/assets/docs/python/flask/peek-definition.png" alt="Peek definition showing the Flask class inline"></p>
</li>
</ul>
<h2 id="_use-a-template-to-render-a-page" data-needslink="_use-a-template-to-render-a-page">Use a template to render a page</h2>
<p>The app you've created so far in this tutorial generates only plain text web pages from Python code. Although it's possible to generate HTML directly in code, developers typically avoid such a practice because it's vulnerable to cross-site scripting (XSS) attacks. Instead, developers separate HTML markup from the code-generated data that gets inserted into that markup. <strong>Templates</strong> are a common approach to achieve this separation.</p>
<ul>
<li>A template is an HTML file that contains placeholders for values that the code provides at run time. The templating engine takes care of making the substitutions when rendering the page. The code, therefore, concerns itself only with data values and the template concerns itself only with markup.</li>
<li>The default templating engine for Flask is <a href="http://jinja.pocoo.org/" class="external-link" target="_blank">Jinja</a>, which is installed automatically when you install Flask. This engine provides flexible options including template inheritance. With inheritance, you can define a base page with common markup and then build upon that base with page-specific additions.</li>
</ul>
<p>In this section you create a single page using a template. In the sections that follow, you configure the app to serve static files, and then create multiple pages to the app that each contain a nav bar from a base template.</p>
<ol>
<li>
<p>Inside the <code>hello_flask</code> folder, create a folder named <code>templates</code>, which is where Flask looks for templates by default.</p>
</li>
<li>
<p>In the <code>templates</code> folder, create a file named <code>hello_there.html</code> with the contents below. This template contains two placeholders named &quot;title&quot; and &quot;content&quot;, which are delineated by pairs of curly braces, <code>{{</code> and <code>}}</code>.</p>
<pre><code class="html"><span class="hljs-doctype">&lt;!DOCTYPE html&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">meta</span> <span class="hljs-attribute">charset</span>=<span class="hljs-value">"utf-8"</span> /&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">title</span>&gt;</span>{{ title }}<span class="hljs-tag">&lt;/<span class="hljs-title">title</span>&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>
        {{ content }}
    <span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span>
</code></pre>
</li>
<li>
<p>In <code>app.py</code>, import Flask's <code>render_template</code> function near the top of the file:</p>
<pre><code class="python"><span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> render_template
</code></pre>
</li>
<li>
<p>Also in <code>app.py</code>, modify the <code>hello_there</code> function to use <code>render_template</code> to load a template and apply the named values. <code>render_template</code> assumes that the first argument is relative to the <code>templates</code> folder. Typically, developers name the templates the same as the functions that use them, but matching names are not required because you always refer to the exact filename in your code.</p>
<pre><code class="python"><span class="hljs-decorator">@app.route("/hello/&lt;name&gt;")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">hello_there</span><span class="hljs-params">(name)</span>:</span>
    now = datetime.now()
    formatted_now = now.strftime(<span class="hljs-string">"%A, %d %B, %Y at %X"</span>)

    <span class="hljs-comment"># BAD CODE! Avoid inline HTML for security reason, plus templates automatically escape HTML content.</span>
    content = <span class="hljs-string">"&lt;strong&gt;Hello there, "</span> + name + <span class="hljs-string">"!&lt;/strong&gt; It's "</span> + formatted_now

    <span class="hljs-keyword">return</span> render_template(
        <span class="hljs-string">"hello_there.html"</span>,
        title=<span class="hljs-string">"Hello, Flask"</span>,
        content=content
    )
</code></pre>
</li>
<li>
<p>Start the program (inside or outside of the debugger, using <span class="dynamic-keybinding" data-osx="⌃F5" data-win="Ctrl+F5" data-linux="Ctrl+F5"><span class="keybinding">⌃F5</span> (Windows, Linux <span class="keybinding">Ctrl+F5</span>)</span>), navigate to a /hello/name URL, and observe the results. Notice that the inline HTML, if you happen to write bad code like this, doesn't get rendered as HTML because the templating engine automatically escapes values used in placeholders. Automatic escaping prevent accidental vulnerabilities to injection attacks: developers often gather input from one page, or the URL, and use it as a value in another page through a template placeholder. Escaping also serves as a reminder that it's again best to keep HTML out of the code entirely.</p>
<p>For this reason, modify the template and view function as follows to make each piece of content more specifically. While you're at it, also move more of the text (including the title) and formatting concerns into the template:</p>
<p>In <code>templates/hello_there.html</code>:</p>
<pre><code class="html"><span class="hljs-doctype">&lt;!DOCTYPE html&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">meta</span> <span class="hljs-attribute">charset</span>=<span class="hljs-value">"utf-8"</span> /&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">title</span>&gt;</span>Hello, Flask<span class="hljs-tag">&lt;/<span class="hljs-title">title</span>&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">strong</span>&gt;</span>Hello there, {{ name }}!<span class="hljs-tag">&lt;/<span class="hljs-title">strong</span>&gt;</span> It's {{ date.strftime("%A, %d %B, %Y at %X") }}.
    <span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span>
</code></pre>
<p>In <code>app.py</code>:</p>
<pre><code class="python"><span class="hljs-decorator">@app.route("/hello/&lt;name&gt;")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">hello_there</span><span class="hljs-params">(name)</span>:</span>
    <span class="hljs-keyword">return</span> render_template(
        <span class="hljs-string">"hello_there.html"</span>,
        name=name,
        date=datetime.now()
    )
</code></pre>
<blockquote>
<p><strong>Tip</strong>: Flask developers often use the <a href="https://pythonhosted.org/Flask-Babel/" class="external-link" target="_blank">flask-babel</a> extension for date formatting, rather than <code>strftime</code>, as flask-babel takes locales and timezones into consideration.</p>
</blockquote>
</li>
<li>
<p>Run the app again and navigate to a /hello/name URL to observe the expected result, then stop the app when you're done.</p>
</li>
</ol>
<h2 id="_serve-static-files" data-needslink="_serve-static-files">Serve static files</h2>
<p>Static files are of two types. First are those files like stylesheets to which a page template can just refer directly. Such files can live in any folder in the app, but are commonly placed within a <code>static</code> folder.</p>
<p>The second type are those that you want to address in code, such as when you want to implement an API endpoint that returns a static file. For this purpose, the Flask object contains a built-in method, <code>send_static_file</code>, which generates a response with a static file contained within the app's <code>static</code> folder.</p>
<p>The following sections demonstrate both types of static files.</p>
<h3 id="_refer-to-static-files-in-a-template" data-needslink="_refer-to-static-files-in-a-template">Refer to static files in a template</h3>
<ol>
<li>
<p>In the <code>hello_flask</code> folder, create a folder named <code>static</code>.</p>
</li>
<li>
<p>Within the <code>static</code> folder, create a file named <code>site.css</code> with the following contents. After entering this code, also observe the syntax highlighting that VS Code provide for CSS files, including a color preview:</p>
<pre><code class="css"><span class="hljs-class">.message</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">font-weight</span>:<span class="hljs-value"> <span class="hljs-number">600</span></span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">color</span>:<span class="hljs-value"> blue</span></span>;
}</span>
</code></pre>
</li>
<li>
<p>In <code>templates/hello_there.html</code>, add the following line before the <code>&lt;/head&gt;</code> tag, which creates a reference to the stylesheet.</p>
<pre><code class="html"><span class="hljs-tag">&lt;<span class="hljs-title">link</span> <span class="hljs-attribute">rel</span>=<span class="hljs-value">"stylesheet"</span> <span class="hljs-attribute">type</span>=<span class="hljs-value">"text/css"</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"{{ url_for('static', filename='site.css')}}"</span> /&gt;</span>
</code></pre>
<p>Flask's <a href="http://flask.pocoo.org/docs/0.12/api/#flask.url_for" class="external-link" target="_blank"><code>url_for</code> tag</a> that's used here creates the appropriate path to the file. Because it can accept variables as arguments, <code>url_for</code> allows you to programmatically control the generated path, if desired.</p>
</li>
<li>
<p>Also in <code>templates/hello_there.html</code>, replace the contents <code>&lt;body&gt;</code> element with the following markup that uses the <code>message</code> style instead of a <code>&lt;strong&gt;</code> tag:</p>
<pre><code class="html"><span class="hljs-tag">&lt;<span class="hljs-title">span</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"message"</span>&gt;</span>Hello, there {{ name }}!<span class="hljs-tag">&lt;/<span class="hljs-title">span</span>&gt;</span>. It's {{ date.strftime("%A, %d %B, %Y at %X") }}.
</code></pre>
</li>
<li>
<p>Run the app, navigate to a /hello/name URL, and observe that the message renders in blue. Stop the app when you're done.</p>
</li>
</ol>
<h3 id="_serve-a-static-file-from-code" data-needslink="_serve-a-static-file-from-code">Serve a static file from code</h3>
<ol>
<li>
<p>In the <code>static</code> folder, create a JSON data file named <code>data.json</code> with the following contents (which are just meaningless sample data):</p>
<pre><code class="json">{
    "<span class="hljs-attribute">01</span>": <span class="hljs-value">{
        "<span class="hljs-attribute">note</span>" : <span class="hljs-value"><span class="hljs-string">"This data is very simple because we're demonstrating only the mechanism."</span>
    </span>}
</span>}
</code></pre>
</li>
<li>
<p>In <code>app.py</code>, add a function with the route /api/data that returns the static data file using the <code>send_static_file</code> method:</p>
<pre><code class="python"><span class="hljs-decorator">@app.route("/api/data")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">get_data</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> app.send_static_file(<span class="hljs-string">"data.json"</span>)
</code></pre>
</li>
<li>
<p>Run the app and navigate to the /api/data endpoint to see that the static file is returned. Stop the app when you're done.</p>
</li>
</ol>
<h2 id="_create-multiple-templates-that-extend-a-base-template" data-needslink="_create-multiple-templates-that-extend-a-base-template">Create multiple templates that extend a base template</h2>
<p>Because most web apps have more than one page, and because those pages typically share many common elements, developers separate those common elements into a base page template that other page templates can then extend. (This is also called template inheritance.)</p>
<p>Also, because you'll likely create many pages that extend the same template, it's helpful to create a code snippet in VS Code with which you can quickly initialize new page templates. A snippet helps you avoid tedious and error-prone copy-paste operations.</p>
<p>The following sections walk through different parts of this process.</p>
<h3 id="_create-a-base-page-template-and-styles" data-needslink="_create-a-base-page-template-and-styles">Create a base page template and styles</h3>
<p>A base page template in Flask contains all the shared parts of a set of pages, including references to CSS files, script files, and so forth. Base templates also define one or more <strong>block</strong> tags that other templates that extend the base are expected to override. A block tag is delineated by <code>{% block &lt;name&gt; %}</code> and <code>{% endblock %}</code> in both the base template and extended templates.</p>
<p>The following steps demonstrate creating a base template.</p>
<ol>
<li>
<p>In the <code>templates</code> folder, create a file named <code>layout.html</code> with the contents below, which contains blocks named &quot;title&quot; and &quot;content&quot;. As you can see, the markup defines a simple nav bar structure with links to Home, About, and Contact pages, which you create in a later section. Each link again uses Flask's <code>url_for</code> tag to generate a link at runtime for the matching route.</p>
<pre><code class="html"><span class="hljs-doctype">&lt;!DOCTYPE html&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">meta</span> <span class="hljs-attribute">charset</span>=<span class="hljs-value">"utf-8"</span> /&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">title</span>&gt;</span>{% block title %}{% endblock %}<span class="hljs-tag">&lt;/<span class="hljs-title">title</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">link</span> <span class="hljs-attribute">rel</span>=<span class="hljs-value">"stylesheet"</span> <span class="hljs-attribute">type</span>=<span class="hljs-value">"text/css"</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"{{ url_for('static', filename='site.css')}}"</span> /&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>

    <span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"navbar"</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"{{ url_for('home') }}"</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"navbar-brand"</span>&gt;</span>Home<span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"{{ url_for('about') }}"</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"navbar-item"</span>&gt;</span>About<span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"{{ url_for('contact') }}"</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"navbar-item"</span>&gt;</span>Contact<span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>
        <span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>

        <span class="hljs-tag">&lt;<span class="hljs-title">div</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"body-content"</span>&gt;</span>
            {% block content %}
            {% endblock %}
            <span class="hljs-tag">&lt;<span class="hljs-title">hr</span>/&gt;</span>
            <span class="hljs-tag">&lt;<span class="hljs-title">footer</span>&gt;</span>
                <span class="hljs-tag">&lt;<span class="hljs-title">p</span>&gt;</span>&amp;copy; 2018<span class="hljs-tag">&lt;/<span class="hljs-title">p</span>&gt;</span>
            <span class="hljs-tag">&lt;/<span class="hljs-title">footer</span>&gt;</span>
        <span class="hljs-tag">&lt;/<span class="hljs-title">div</span>&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span>
</code></pre>
</li>
<li>
<p>Add the following styles to <code>static/site.css</code> below the existing &quot;message&quot; style, and save the file. (This walkthrough doesn't attempt to demonstrate responsive design; these styles simply generate a reasonably interesting result.)</p>
<pre><code class="css"><span class="hljs-class">.navbar</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">background-color</span>:<span class="hljs-value"> lightslategray</span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">font-size</span>:<span class="hljs-value"> <span class="hljs-number">1em</span></span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">font-family</span>:<span class="hljs-value"> <span class="hljs-string">'Trebuchet MS'</span>, <span class="hljs-string">'Lucida Sans Unicode'</span>, <span class="hljs-string">'Lucida Grande'</span>, <span class="hljs-string">'Lucida Sans'</span>, Arial, sans-serif</span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">color</span>:<span class="hljs-value"> white</span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">padding</span>:<span class="hljs-value"> <span class="hljs-number">8px</span> <span class="hljs-number">5px</span> <span class="hljs-number">8px</span> <span class="hljs-number">5px</span></span></span>;
}</span>

<span class="hljs-class">.navbar</span> <span class="hljs-tag">a</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">text-decoration</span>:<span class="hljs-value"> none</span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">color</span>:<span class="hljs-value"> inherit</span></span>;
}</span>

<span class="hljs-class">.navbar-brand</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">font-size</span>:<span class="hljs-value"> <span class="hljs-number">1.2em</span></span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">font-weight</span>:<span class="hljs-value"> <span class="hljs-number">600</span></span></span>;
}</span>

<span class="hljs-class">.navbar-item</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">font-variant</span>:<span class="hljs-value"> small-caps</span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">margin-left</span>:<span class="hljs-value"> <span class="hljs-number">30px</span></span></span>;
}</span>

<span class="hljs-class">.body-content</span> <span class="hljs-rules">{
    <span class="hljs-rule"><span class="hljs-attribute">padding</span>:<span class="hljs-value"> <span class="hljs-number">5px</span></span></span>;
    <span class="hljs-rule"><span class="hljs-attribute">font-family</span>:<span class="hljs-value"><span class="hljs-string">'Segoe UI'</span>, Tahoma, Geneva, Verdana, sans-serif</span></span>;
}</span>
</code></pre>
</li>
</ol>
<p>You can run the app at this point, but because you haven't made use of the base template anywhere and haven't changed any code files, the result is the same as the previous step. Complete the remaining sections to see the final effect.</p>
<h3 id="_create-a-code-snippet" data-needslink="_create-a-code-snippet">Create a code snippet</h3>
<p>Because the three pages you create in the next section extend <code>layout.html</code>, it saves time to create a <strong>code snippet</strong> to initialize a new template file with the appropriate reference to the base template. A code snippet provides a consistent piece of code from a single source, which avoids errors that can creep in when using copy-paste from existing code.</p>
<ol>
<li>
<p>In VS Code, select the <strong>File</strong> (Windows/Linux) or <strong>Code</strong> (macOS), menu, then select <strong>Preferences</strong> &gt; <strong>User snippets</strong>.</p>
</li>
<li>
<p>In the list that appears, select <strong>html</strong>. (The option may appear as &quot;html.json&quot; in the <strong>Existing Snippets</strong> section of the list if you've created snippets previously.)</p>
</li>
<li>
<p>After VS code opens <code>html.json</code>, add the following entry within the existing curly braces (the explanatory comments, not shown here, describe details such as how the <code>$0</code> line indicates where VS Code places the cursor after inserting a snippet):</p>
<pre><code class="json"><span class="hljs-string">"Flask App: template extending layout.html"</span>: {
    "<span class="hljs-attribute">prefix</span>": <span class="hljs-value"><span class="hljs-string">"flextlayout"</span></span>,
    "<span class="hljs-attribute">body</span>": <span class="hljs-value">[
        <span class="hljs-string">"{% extends \"layout.html\" %}"</span>,
        <span class="hljs-string">"{% block title %}"</span>,
        <span class="hljs-string">"$0"</span>,
        <span class="hljs-string">"{% endblock %}"</span>,
        <span class="hljs-string">"{% block content %}"</span>,
        <span class="hljs-string">"{% endblock %}"</span>
    ]</span>,

    "<span class="hljs-attribute">description</span>": <span class="hljs-value"><span class="hljs-string">"Boilerplate template that extends layout.html"</span>
</span>},
</code></pre>
</li>
<li>
<p>Save the <code>html.json</code> file (<span class="dynamic-keybinding" data-osx="⌘S" data-win="Ctrl+S" data-linux="Ctrl+S"><span class="keybinding">⌘S</span> (Windows, Linux <span class="keybinding">Ctrl+S</span>)</span>).</p>
</li>
<li>
<p>Now, whenever you start typing the snippet's prefix, such as <code>flext</code>, VS Code provides the snippet as an autocomplete option, as shown in the next section. You can also use the <strong>Insert Snippet</strong> command to choose a snippet from a menu.</p>
</li>
</ol>
<p>For more information on code snippets in general, refer to <a href="/docs/editor/userdefinedsnippets">Creating snippets</a>.</p>
<h3 id="_use-the-code-snippet-to-add-pages" data-needslink="_use-the-code-snippet-to-add-pages">Use the code snippet to add pages</h3>
<p>With the code snippet in place, you can quickly create templates for the Home, About, and Contact pages.</p>
<ol>
<li>
<p>In the <code>templates</code> folder, create a new file named <code>home.html</code>, Then start typing <code>flext</code> to see the snippet appear as a completion:</p>
<p><img src="/assets/docs/python/flask/autocomplete-for-code-snippet.png" alt="Autocompletion for the flextlayout code snippet"></p>
<p>When you select the completion, the snippet's code appears with the cursor on the snippet's insertion point:</p>
<p><img src="/assets/docs/python/flask/code-snippet-inserted.png" alt="Insertion of the flextlayout code snippet"></p>
</li>
<li>
<p>At the insertion point in the &quot;title&quot; block, write <code>Home</code>, and in the &quot;content&quot; block, write <code>&lt;p&gt;Home page for the Visual Studio Code Flask tutorial.&lt;/p&gt;</code>, then save the file. These lines are the only unique parts of the extended page template:</p>
</li>
<li>
<p>In the <code>templates</code> folder, create <code>about.html</code>, use the snippet to insert the boilerplate markup, insert <code>About us</code> and <code>&lt;p&gt;About page for the Visual Studio Code Flask tutorial.&lt;/p&gt;</code> in the &quot;title&quot; and &quot;content&quot; blocks, respectively, then save the file.</p>
</li>
<li>
<p>Repeat the previous step to create <code>templates/contact.html</code> using <code>Contact us</code> and <code>&lt;p&gt;Contact page for the Visual Studio Code Flask tutorial.&lt;/p&gt;</code> in the two content blocks.</p>
</li>
<li>
<p>In <code>app.py</code>, add functions for the /about and /contact routes that refer to their respective page templates. Also modify the <code>home</code> function to use the <code>home.html</code> template.</p>
<pre><code class="python"><span class="hljs-comment"># Replace the existing home function with the one below</span>
<span class="hljs-decorator">@app.route("/")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">home</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"home.html"</span>)

<span class="hljs-comment"># New functions</span>
<span class="hljs-decorator">@app.route("/about")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">about</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"about.html"</span>)

<span class="hljs-decorator">@app.route("/contact")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">contact</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"contact.html"</span>)
</code></pre>
</li>
</ol>
<h3 id="_run-the-app" data-needslink="_run-the-app">Run the app</h3>
<p>With all the page templates in place, save <code>app.py</code>, run the app, and open a browser to see the results. Navigate between the pages to verify that the page template are properly extending the base template.</p>
<p><img src="/assets/docs/python/flask/full-app.png" alt="Flask app rendering a common nav bar from the base template"></p>
<h2 id="_optional-activities" data-needslink="_optional-activities">Optional activities</h2>
<p>The following sections describe additional steps that you might find helpful in your work with Python and Visual Studio Code.</p>
<h3 id="_create-a-requirementstxt-file-for-the-environment" data-needslink="_create-a-requirementstxt-file-for-the-environment">Create a requirements.txt file for the environment</h3>
<p>When you share your app code through source control or some other means, it doesn't make sense to copy all the files in a virtual environment because recipients can always recreate the environment themselves.</p>
<p>Accordingly, developers typically omit the virtual environment folder from source control and instead describe the app's dependencies using a <code>requirements.txt</code> file.</p>
<p>Although you can create the file by hand, you can also use the <code>pip freeze</code> command to generate the file based on the exact libraries installed in the activated environment:</p>
<ol>
<li>
<p>With your chosen environment selected using the <strong>Python: Select Interpreter</strong> command, run the <strong>Terminal: Create New Integrated Terminal</strong> command (<span class="dynamic-keybinding" data-osx="⌃⇧`" data-win="Ctrl+Shift+`" data-linux="Ctrl+Shift+`"><span class="keybinding">⌃⇧`</span> (Windows, Linux <span class="keybinding">Ctrl+Shift+`</span>)</span>)) to open a terminal with that environment activated.</p>
</li>
<li>
<p>In the terminal, run <code>pip freeze &gt; requirements.txt</code> to create the <code>requirements.txt</code> file in your project folder.</p>
</li>
</ol>
<p>Anyone (or any build server) that receives a copy of the project needs only to run the <code>pip install -r requirements.txt</code> command to reinstall the packages in the original the environment. (The recipient still needs to create their own virtual environment, however.)</p>
<blockquote>
<p><strong>Note</strong>: <code>pip freeze</code> lists all the Python packages you have installed in the current environment, including packages you aren't currently using. The command also lists packages with exact version numbers, which you might want to convert to ranges for more flexibility in the future. For more information, see <a href="https://pip.readthedocs.io/en/stable/user_guide/#requirements-files" class="external-link" target="_blank">Requirements files</a> in the pip command documentation.</p>
</blockquote>
<h3 id="_refactor-the-project-to-support-further-development" data-needslink="_refactor-the-project-to-support-further-development">Refactor the project to support further development</h3>
<p>Throughout this tutorial, all the app code is contained in a single <code>app.py</code> file. To allow for further development and to separate concerns, it's helpful to refactor the pieces of <code>app.py</code> into separate files.</p>
<ol>
<li>
<p>In your project folder, create a folder for the app, such as <code>hello_app</code>, to separate its files from other project-level files like <code>requirements.txt</code> and the <code>.vscode</code> folder where VS Code stores settings and debug configuration files.</p>
</li>
<li>
<p>Move the <code>static</code> and <code>templates</code> folders into <code>hello_app</code>, because these folders certainly contain app code.</p>
</li>
<li>
<p>In the <code>hello_app</code> folder, create a file named <code>views.py</code> that contains the routings and the view functions:</p>
<pre><code class="python"><span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> Flask
<span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> render_template
<span class="hljs-keyword">from</span> datetime <span class="hljs-keyword">import</span> datetime
<span class="hljs-keyword">from</span> . <span class="hljs-keyword">import</span> app

<span class="hljs-decorator">@app.route("/")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">home</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"home.html"</span>)

<span class="hljs-decorator">@app.route("/about")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">about</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"about.html"</span>)

<span class="hljs-decorator">@app.route("/contact")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">contact</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> render_template(<span class="hljs-string">"contact.html"</span>)

<span class="hljs-decorator">@app.route("/hello/&lt;name&gt;")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">hello_there</span><span class="hljs-params">(name)</span>:</span>
    <span class="hljs-keyword">return</span> render_template(
        <span class="hljs-string">"hello_there.html"</span>,
        name=name,
        date=datetime.now()
    )

<span class="hljs-decorator">@app.route("/api/data")</span>
<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">get_data</span><span class="hljs-params">()</span>:</span>
    <span class="hljs-keyword">return</span> app.send_static_file(<span class="hljs-string">"data.json"</span>)
</code></pre>
</li>
<li>
<p>Optional: Right-click in the editor and select the <strong>Sort Imports</strong> command, which consolidates imports from identical modules, removes unused imports, and sorts your import statements. Using the command on the code above in <code>views.py</code> changes the imports as follows (you can remove the extra lines, of course):</p>
<pre><code class="python"><span class="hljs-keyword">from</span> datetime <span class="hljs-keyword">import</span> datetime

<span class="hljs-keyword">from</span> flask <span class="hljs-keyword">import</span> Flask, render_template

<span class="hljs-keyword">from</span> . <span class="hljs-keyword">import</span> app
</code></pre>
</li>
<li>
<p>In the <code>hello_app</code> folder, create a file <code>__init__.py</code> with the following contents:</p>
<pre><code class="python"><span class="hljs-keyword">import</span> flask
app = flask.Flask(__name__)
</code></pre>
</li>
<li>
<p>In the <code>hello_app</code> folder, create a file <code>webapp.py</code> with the following contents:</p>
<pre><code class="python"><span class="hljs-comment"># Entry point for the application.</span>
<span class="hljs-keyword">from</span> . <span class="hljs-keyword">import</span> app    <span class="hljs-comment"># For application discovery by the 'flask' command.</span>
<span class="hljs-keyword">from</span> . <span class="hljs-keyword">import</span> views  <span class="hljs-comment"># For import side-effects of setting up routes.</span>
</code></pre>
</li>
<li>
<p>Open the debug configuration file <code>launch.json</code> and update the <code>env</code> property as follows to point to the startup object:</p>
<pre><code class="json"><span class="hljs-string">"env"</span>: {
    "<span class="hljs-attribute">FLASK_APP</span>": <span class="hljs-value"><span class="hljs-string">"hello_app.webapp"</span>
</span>},
</code></pre>
</li>
<li>
<p>Delete the original <code>app.py</code> file in the project root, as its contents have been moved into other app files.</p>
</li>
<li>
<p>Your project's structure should now be similar to the following:</p>
<p><img src="/assets/docs/python/flask/project-structure.png" alt="Modified project structure with separate files and folders for parts of the app"></p>
</li>
<li>
<p>Run the app in the debugger again to make sure everything works. To run the app outside of the VS Code debugger, use the following steps:</p>
<ol>
<li>Set an environment variable for <code>FLASK_APP</code>. On Linux and macOS, use <code>export set FLASK_APP=webapp</code>; on Windows use <code>set FLASK_APP=webapp</code>.</li>
<li>In the <code>hello_app</code> folder, launch the program using <code>python3 -m flask run</code> (Linux/macOS) or <code>python -m flask run</code> (Windows).</li>
</ol>
</li>
</ol>
<p>If you have any problems, feel free to file an issue for this tutorial in the <a href="https://github.com/Microsoft/vscode-docs/issues" class="external-link" target="_blank">VS Code documentation repository</a>.</p>
<h2 id="_next-steps" data-needslink="_next-steps">Next steps</h2>
<p>Congratulations on completing this walkthrough of working with Flask in Visual Studio Code!</p>
<p>The completed code project from this tutorial can be found on GitHub: <a href="https://github.com/Microsoft/python-sample-vscode-flask-tutorial" class="external-link" target="_blank">python-sample-vscode-flask-tutorial</a>.</p>
<p>Because this tutorial has only scratched the surface of page templates, refer to the <a href="http://jinja.pocoo.org/docs/" class="external-link" target="_blank">Jinja2 documentation</a> for more information about templates. The <a href="http://jinja.pocoo.org/docs/templates/#synopsis" class="external-link" target="_blank">Template Designer Documentation</a> contains all the details on the template language.</p>
<p>To try your app on a production website, check out the tutorial <a href="/docs/python/tutorial-deploy-containers">Deploy Python apps to Azure App Service using Docker Containers</a>. Azure also offers a standard container, <a href="/docs/python/tutorial-deploy-app-service-on-linux">App Service on Linux (Preview)</a>, to which you deploy web apps from within VS Code.</p>
<p>You may also want to review the following articles in the VS Code docs that are relevant to Python:</p>
<ul>
<li><a href="/docs/python/editing">Editing Python code</a></li>
<li><a href="/docs/python/linting">Linting</a></li>
<li><a href="/docs/python/environments">Managing Python environments</a></li>
<li><a href="/docs/python/debugging">Debugging Python</a></li>
<li><a href="/docs/python/unit-testing">Unit testing</a></li>
</ul>
<p>If you encountered any problems in the course of this tutorial, feel free to file an issue in the <a href="https://github.com/Microsoft/vscode-docs/issues" class="external-link" target="_blank">VS Code documentation repository</a>.</p>
