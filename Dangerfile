# coding: utf-8
# -*- mode: ruby -*-
pep8.lint

MARKDOWN_TEMPLATE = '## isort found issues\n'

errors = []
git.modified_files.each do |file|
  modified = `isort -df #{file}` if File.extname(file) == ".py"
  errors << { file: file, diff: modified } if modified
end

if errors.length > 0
  report = errors.inject(MARKDOWN_TEMPLATE) do |out, err|
    link = github.html_link("#{err[:file]}", full_path: false)
    out += "* #{link}\n"
    out += "```diff\n#{err[:diff]}\n```\n"
  end
  markdown(report)
  fail('isortのエラーを修正してください')
end
