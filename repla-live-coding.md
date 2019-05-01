# Repla: A New-Old Programming Tool

How to make new innovating programming tools that work with existing tools and workflows.

Repla as an example.

---

# Who Am I

Roben Kleene

1. Developer for Apple platforms (iOS & Mac)
2. Left job managing WSJ app team to make my own programming app
3. I like AppKit GUI apps, and Unix TUI apps
4. Not a researcher, trying to create a business
5. [@robenkleene](https://twitter.com/robenkleene)
6. [robenkleene.com](https://robenkleene.com)

---

# Poll

![fit](assets/poll.png)

---

# Traits of Successful Programming Tools

(For existing programmers)

- **Language Agnostic**: Work with existing programming languages
- **Plain Text**: An open data format
- **Packages Written in Scripting Languages**: Make customizations easy to share and modify
- **Text Editors**: The center for programming man-hours
- **Browser Rendering Engine**: A lingua franca for graphics
- **Unix Processes**: Use child processes to extend capabilities
- **Version Control**: State of the art collaboration

---

# Case Study: Visual Studio Code

Visual Studio Code is a **language agnostic** **plain text editor** used to edit files that can be stored in **version control**. It's user interface is displayed using a **browser rendering engine**. It's **packages are written in scripting languages** that launch **Unix processes**.

## Market Share

- **2016:** 7.2%
- **2017:** 22.3%
- **2018:** 34.9%
- **2019:** 50.7%
<64;28;44M
- According to [Stack Overflow Insights](https://insights.stackoverflow.com/)
- Competes with text editors: [20-25 employees](https://changelog.com/podcast/277).

---

# What is Repla?

- A web rendering engine
- Unix process management
- A packaging system

# What it isn't?

- It is not an editor, generally tries to work along-side existing editors?

---

- Screenshot
- Animated GIFs
- Website renders

## Use Cases

1. Processes: Web Development (An automatically refreshing browser)
2. Packaging System: Distributing Web Apps (One click install, one click run Jupyter Notebooks)
3. Packages: Live Coding View
4. Packages: Framer Classic & Processing

---

# Why Not an IDE?

- Don't put these features in an IDE
- 23 people working on visual studio code

- A tool that shapes itself to the problem

---

# Fitting into existing workflows

- Developers work with an editor, a terminal, and a browser, replacing the browser.
- Not as crazy as it sounds, an editor and a terminal do the same things, they both manage child processes.

---

# Inspiration

- Skipping Bret Victor and Light Table
- Soulver
- Swift Playgrounds
- Literate CoffeeScript
- Emacs `C-x C-e`, `(split-window-vertically)`
- REPL integration, do the same with `IRB`, via an "inferior" process
- Marked

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

## Details

- The Ruby process watches the file system
- `gem 'listen'`
