# -*- mode: ruby -*-
pep8.lint


MARKDOWN_TEMPLATE = <<EOF
## isort found issues :danger:
EOF

errors = []
git.modified_files.each do |file|
  `isort #{file}`

  is_modified = `git diff #{file} | wc -l`.strip.to_i > 0
  errors << "#{file}" if is_modified
end

if errors.length > 0
  report = errors.inject(MARKDOWN_TEMPLATE) do |out, file|
    out += "* #{file}\n"
  end

  markdown(report)
end

