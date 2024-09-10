EigenGen
========

EigenGen is a command line driven code generator. It works with 
  - Anthropic claude-3-5-sonnet
  - OpenAI GPT4o


You must
```
export ANTHROPIC_API_KEY=<your-api-key>
or
export OPENAI_API_KEY=<your-api-key>
```

and then create a venv and install this package with:
```
python3 -m venv .venv
. .venv/bin/activate
pip install -e .
```

Example Usage:
```
# add new review feature and apply it blindly with patch -p1
eigengen --diff --file eigengen/eigengen.py "Add --review flag and make it write a code review for the file given with --file argument. Please implement this by having --review fill in a default prompt with text 'Please write a code review for the given file'. --review should not be used together with --diff flag." | patch -p1

# pipe file content in through stdin
cat setup.py | eigengen --file - "Please review the given source file, thank you!"

# pipe a git diff output and write a review for it
git diff origin/main^^..HEAD | eigengen --file - "Please write a code review for the given diff, thank you!
```

By default eigengen uses claude-3-5-sonnet. In order to use OpenAI GPT4o model, please give --model-alias argument
like this:
```
eigengen --model-alias gpt4 "your prompt content"
```

You may wish to create a shell alias to avoid having to type it in all the time:
```.bashrc
alias eigengen='eigengen --model-alias gpt4'
```

Pull Requests are welcome!
