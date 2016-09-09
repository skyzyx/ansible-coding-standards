# Ansible/YAML Coding Standards

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

You are encouraged to add the dotfiles from this repository to your project, and use an editor/IDE which understands them — otherwise, know how to apply these rules to your files manually.

## Elements of a good playbook

* YAML documents (including Ansible playbooks) MUST begin a document with `---` followed by one empty line.

  ```yaml
  ---
  
  # Begin playbook...
  ```

* Every task MUST have a `name`.

* Every task MUST have 1 or more appropriate tags, annotated as an array instead of a single string.

  ```yaml
  # Good
  tags:
    - abc

  # Bad
  tags: abc
  ```

* You SHOULD use the built-in Ansible task (when available) instead of simply calling-out to the shell. See [Ansible: List of all modules](http://docs.ansible.com/ansible/list_of_all_modules.html) for more information. In certain cases, Ansible actions are not yet powerful enough to replace Bash actions.

* Any use of `when` SHOULD happen _after_ the primary action (e.g., "do this thing _when_ this condition is met").

* Binary decisions MUST use `yes`/`no` instead of `true`/`false`.

## Editor Settings

* Indentation should be 2 spaces. Further, arrays (i.e., lines which begin with `-`) should be indented 2 spaces from its parent as well.

* Line-endings MUST use the `\n` character (`LF`) used by default on Mac OS X and *nix systems.

* Lines MUST NOT have trailing whitespace.

* A file MUST end with a single empty line feed.

* Files MUST use only UTF-8 _without_ BOM as its character encoding.

## Whitespace

* Files SHOULD have soft-limit of `80` characters per line. Valid exceptions are when you have an unbreaking line.

* Files SHOULD use long-form YAML, not short-form YAML.

  ```yaml
  # Good
  - name: Make new symlink
    file:
      state: link
      owner: root
      group: root
      src: /usr/local/okapi/{{ version }}
      path: /usr/local/okapi/okapi_new

  # Bad
  - name: Make new symlink
    file: state=link owner=root group=root src=/usr/local/okapi/{{ version }} path=/usr/local/okapi/okapi_new
  ```

## Comments

* Non-documentation comments are strongly encouraged. A general rule of thumb is that if you look at a section of code and think "Wow, I don't want to try and describe that", you need to comment it before you forget how it works.

* For readability, comments MUST have a single space after `#`.

  ```yaml
  # Good Comment
  
  #Bad Comment
  #    Bad Comment
  #  Bad Comment
  ```

* There SHOULD always be one line of whitespace above the start of a comment block.

  ```yaml
  # This is my code.
  key: ansible_command
  
  # This is more code.
  key: another_ansible_command
  ```

* For inline comments (e.g., commenting-out a line), the comment MUST begin after the appropriate indentation, prefixing the line with a `# ` (hash-space). You MUST NOT add a `#` to the beginning of a line, being irrespective of indentation.

  ```yaml
  # Good
  abc:
    def:
      # - 123
      - 456
      - 789

  # Bad
  abc:
    def:
  #    - 123
      - 456
      - 789
  ```

## Spelling

If there is ever a discrepancy between English-speaking dialects, use **U.S. English** as a baseline for both spelling and word choice. [Grammarist](http://grammarist.com/spelling/) and similar websites can help ensure intended usage.

```
color (correct)
colour (incorrect)

spelled (correct)
spelt (incorrect)

canceled (correct)
cancelled (incorrect)

labeled (correct)
labelled (incorrect)

math (correct)
maths (incorrect)

apartment (correct)
flat (incorrect)

"Apple is very successful." (correct)
"Apple are very successful." (incorrect)
```
