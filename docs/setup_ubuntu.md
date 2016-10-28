Linux Setup
===========

## Starting a terminal

For these instructions, and for much of the class, you will need to have a terminal, or command line, open. This is a text-based interface to talk to your computer, and you can open it by clicking "Dash Home" and typing `Terminal`. You can also open a terminal at any time by pressing `CTRL-ALT-T`. If you have never used the terminal before, you may want to spend some time [reading up on command-line basics](http://blog.teamtreehouse.com/command-line-basics).

Go ahead and open your terminal now. It should look something like this:

![blank terminal](img/ubuntu/blank_terminal.png)

The prompt (where you will type your commands) may look different: it usually shows the computer name and user name, as well as the folder or directory you are currently in.

For the rest of this setup, I will tell you to run commands in your terminal. When I say that, I mean "type the command into the terminal and press the Return key."

## Install Java

Instructions vary by Linux distribution... For Debian and Ubuntu you
can update the package manager and install OpenJDK 8 like this:

```
# apt-get update
# apt-get install openjdk-8-jdk
```

When Java is installed, you will see something like this in your terminal:

```
clojurista@mylaptop $ java -version
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-8u111-b14-2-b14)
OpenJDK 64-Bit Server VM (build 25.111-b14, mixed mode)
clojurista@mylaptop $
```

The details of Java's version may differ from what you see above; that is perfectly fine.

## Installing Nightcode

On the [Nightcode home page](https://sekao.net/nightcode/) you can download
and install a `*.deb` for Debian/Ubuntu, `*.rpm` for RedHat/Fedora,
or `*.jar` file for any other distribution.

If you download the `*.jar` you can place it in your `~/bin` directory and
use our handy launcher script. NOTE: for this method we also install the
Clojure jar here to get started:

```
clojurista@mylaptop $ cd ~/bin
clojurista@mylaptop $ mv ~/Downloads/Nightcode*.jar ./
clojurista@mylaptop $ curl -O http://repo1.maven.org/maven2/org/clojure/clojure/1.8.0/clojure-1.8.0.zip
clojurista@mylaptop $ unzip clojure-1.8.0.zip
clojurista@mylaptop $ curl -O https://raw.githubusercontent.com/clojurebridge-minneapolis/installfest/master/bin/nightcode
clojurista@mylaptop $ chmod +x nightcode
```

Now you should be able to launch it by typing `nightcode` in a terminal.


## Installing Leiningen

Leiningen is a tool used on the command line to manage Clojure projects.

Go to the [Leiningen website](http://leiningen.org/). You will see a link to the `lein` script under the "Install" heading. Right-click that link and choose "Save Link As...". Save it in your Downloads directory.

![Leiningen site](img/leiningen_site.png)
![Leiningen site](img/lein_install.png)

After that, run the following commands in your terminal. You will be prompted to enter your password.

```
sudo mkdir -p /usr/local/bin/
sudo mv ~/Downloads/lein* /usr/local/bin/lein
sudo chmod a+x /usr/local/bin/lein
cd $HOME
echo 'PATH=$PATH:/usr/local/bin' >> .bashrc
exec bash
```

After you run the above commands, run the `lein version` command. It should take a while to run, as it will download some resources it needs the first time. If it completes successfully, you are golden! If not, ask an instructor for help.


## Getting setup with Heroku

Heroku is the tool we will use in order to put your application online where others can see it.

First, we need to create an account. Go to [Heroku](http://heroku.com) and click the "Sign up" link.

![Heroku step 1](img/heroku-step1.png)

You will be taken to a form where you need to enter your email address in order to sign up. Fill out that form, and you will be sent an email with a link to click to continue the signup process.

![Heroku step 2](img/heroku-step2.png)

After clicking on the link, you will be taken to another form where you will need to choose a password. Choose one and enter it twice.

![Heroku step 3](img/heroku-step3.png)

After all that, you should be at your Heroku dashboard. There will be a link on the dashboard to download the Heroku Toolbelt. Download it now.

![Heroku dashboard](img/ubuntu/heroku_dashboard_ubuntu.png)

If you do not see this link on your dashboard, you can download the toolbelt from [toolbelt.heroku.com](https://toolbelt.heroku.com/).

This will take you too a page with a terminal command. Copy this command and paste it into your terminal. Once the Heroku Toolbelt is installed, run the command `heroku login`. You will be prompted for your email and password on Heroku. If you are prompted to create an SSH key, say yes. If you enter them and the command ends successfully, congratulations!

## Testing your setup

You have set up Java, Nightcode, Leiningen, Git, and Heroku on your computer--all the tools you will need for this course. Before starting, we need to test them out.

Go to your terminal and run the following command:

```
git clone https://github.com/heroku/clojure-sample.git
```

This will check out a sample Clojure application from GitHub, a central repository for lots of source code. Your terminal should look similar to this picture:

![Testing git clone](img/ubuntu/testing-step1.png)

Then run the command:

```
cd clojure-sample
```

This will put you in the directory with the source code for this sample bit of Clojure code. After that completes, run:

```
lein repl
```

This could take a long time, and will download many other pieces of code it relies on. You should see lines that start with `Retrieving ...` on your screen. When it finishes, your terminal should look like the following:

![Testing lein repl](img/ubuntu/testing-step2.png)

This is starting a REPL, which we will learn about soon. It's a special terminal for Clojure. At the REPL prompt, type `(+ 1 1)` and press Return. Did you get the answer `2` back? You will learn more about that in the course. For now, press the Control button and D button on your keyboard together (abbreviated as Ctrl+D). This should take you out of the Clojure REPL and back to your normal terminal prompt.

**FIXME**

Now, start Light Table. Once it is started, press the Control button and Space Bar together (abbreviated Ctrl+Space). This is how you start giving Light Table a command. Start typing the word "instarepl" and you should see a menu of options, like below. Choose "Instarepl: open a clojure instarepl."

![Testing Light Table - starting instarepl](img/ubuntu/testing-step3.png)

**FIXME**

At the bottom of the screen, you will see a cube moving and some text about connecting and installing dependencies. Once that stops moving, type `(+ 1 1)` into the window. It should look like the following image:

![Testing Light Table - running in the instarepl](img/ubuntu/testing-step4.png)

**FIXME**

If that worked, great! Close Light Table. We only have one more thing to test, Heroku.

Go back to your terminal. You should still be in the `clojure-sample` directory.

Run this command:

`heroku create`

There should be output about something being created. A URL will be displayed. Look at the following example:

![Testing heroku create](img/ubuntu/testing-step5.png)

Next, run the following commands:

```
git push heroku master
heroku open
```

Enter "yes" if you are asked if you are sure you want to connect, like in the following image:

![Connecting via SSH](img/ubuntu/testing-step6.png)

Your browser should open (and take a long time to load), and you should see a website like the following:

![Testing heroku working](img/ubuntu/testing-step7.png)

If your browser does not open after running `heroku open`, start a browser and go to the URL displayed after you ran `heroku create`.

Congratulations! That website is running code you have on your computer that you have uploaded. You have actually made a very simple Clojure app, and your computer is all set up to make more.

## Try the koans

If you're a track 2 student, try to tackle running the [koans](koans.md).
