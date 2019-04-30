# Repla: A Live Coding Tool

## Repla

- Screenshot
- Animated GIFs

## Goals

- Use existing tools, Light Table, need to replace your text editor. Instantly you're competing with some of the most complicated software in existence.
- Compatible with `git`

## Technology

- A web rendering engine
- Unix process management (emphasis on standard input and standard output)
- A packaging system

## Target Audience

- Image of that Slack poll
- Developers work with an editor, a terminal, and a browser, replacing the browser.
- Not as crazy as it sounds, an editor and a terminal do the same things, they both manage child processes.

## Use Cases

1. Processes: Web Development (An automatically refreshing browser)
2. Packaging System: Distributing Web Apps (One click install, one click run Jupyter Notebooks)
3. Packages: Live Coding View
4. Packages: Framer Classic & Processing

## Origins

- Emacs `C-x C-e`, `(split-window-vertically)`
- REPL integration, do the same with `IRB`, via an "inferior" process

### Live Coding

Packages for each language:

- `IRB.replaplugin`, `Python.replaplugin`, `Node.replaplugin`
- Use your existing code editor.

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

## Live Coding

- The Ruby process watches the file system
- `gem 'listen'`

