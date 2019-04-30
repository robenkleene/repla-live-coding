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

## Use Cases

- Web Development (An automatically refreshing browser)
- Distributing Web Apps (One click install, one click run Jupyter Notebooks)
- Live Coding View
- Framer Classic & Processing

## Origins

- Emacs `C-x C-e`, `(split-window-vertically)`
- REPL integration, do the same with `IRB`

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
