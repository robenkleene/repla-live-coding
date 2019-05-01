# Repla: A New-Old Programming Tool

How to make new innovating programming tools that work with existing tools and workflows.

Roben Kleene
[@robenkleene](https://twitter.com/robenkleene)
[robenkleene.com](https://robenkleene.com)

---

# Who Am I

* Developer for Apple platforms (iOS & Mac)
* Currently making a programming tool called Repla
* Left job managing WSJ iOS app team to work on this
* I like AppKit GUI apps, and Unix TUI apps
* Not a researcher, trying to create a business

---

![fit](assets/poll.png)

---

## Traits of Successful Programming Tools (For Existing Programmers) 1/2

- **Browser UI**: A lingua franca for graphics
- **Language Agnostic**: Work with existing programming languages
- **Plain Text**: An open data format
- **Packages Written in Scripting Languages**: Make customizations easy to share and modify

---

## Traits of Successful Programming Tools (For Existing Programmers) 2/2

- **Text Editors**: The concentration of programming man-hours
- **Unix Processes**: Use child processes to extend capabilities
- **Version Control**: State of the art collaboration

---

# Case Study: Visual Studio Code

Visual Studio Code is a **language agnostic** **plain text editor** used to edit files that can be stored in **version control**. It's user interface is displayed using a **browser rendering engine**. It's **packages are written in scripting languages** that launch **Unix processes**.

---

# Visual Studio Code Market Share

- **2016:** 7.2%
- **2017:** 22.3%
- **2018:** 34.9%
- **2019:** 50.7%

[Stack Overflow Insights](https://insights.stackoverflow.com/), competes with text editors: [20-25 employees](https://changelog.com/podcast/277).

---

# What is Repla?

- A web rendering engine
- Unix process management
- A packaging system

# What isn't it?

- An editor

---

# Repla

Instead of re-inventing the wheel, it seeks to work alongside existing tools.

- Developers work with an editor, a terminal, and a browser, replaces the browser for some tasks.
- Not as crazy as it sounds: an editor and a terminal both center on packaging systems and managing child processes.

---

![inline](assets/node.gif)

![inline](assets/irb.gif)

---

![inline](assets/html.gif)

![inline](assets/markdown.gif)

---

![fit](assets/live.png)

---

![fit](assets/repla.png)

---

## Use Cases

1. **Processes:** Web Development (integrate the server and browser into one window, automatically refresh)
2. **Packaging System:** Distributing Web Apps (one click install, one click run, e.g., Jupyter Notebooks)
3. **Packages 1:** Live Coding View
4. **Packages 2:** Framer Classic & Processing

---

# Why Not Integrate With an IDE?

---

![fit](assets/xcode.png)

---

# Inspiration (No Bret Victor or Light Table)

---

![fit](assets/marked.png)

---

# Marked

- Plain text
- Works with text editors
- Works with version control
- But not language agnostic

---

![fit](assets/soulver.png)

---

- Not plain text
- Not language agnostic
- Doesn't work with version control

---

- Observable HQ

---

- Not plain text
- Not language agnostic
- Doesn't work with version control

---

- Swift Playgrounds

---

- Not plain text
- Not language agnostic
- Doesn't work with version control

---

- Literate CoffeeScript

---

- Plain text
- Works with text editors
- Works with version control
- Not language agnostic

---

- Emacs `C-x C-e`, `(split-window-vertically)`
- REPL integration, do the same with `IRB`, via an "inferior" process

---

# Live Coding

Packages for each language:

- `IRB.replaplugin`, `Python.replaplugin`, `Node.replaplugin`
- Use your existing code editor.

---

# Implementation

Managing an `IRB` child process:

      def initialize(command)
        PTY.spawn(command) do |output, input, _pid|
          Thread.new do
            output.each do |line|
              output_controller.parse_output(line)
            end
          end
          @input = input
        end
      end

      def parse_input(input)
        input_controller.parse_input(input)
        write_input(input)
      end

      def write_input(input)
        @input.write(input)
      end

---

## Details

- The Ruby process watches the file system
- `gem 'listen'`

---

Thanks!

Roben Kleene
[@robenkleene](https://twitter.com/robenkleene)
[robenkleene.com](https://robenkleene.com)
