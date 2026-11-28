# LifeDB Plugin

This plugin lets an AI assistant answer questions about your own messages, conversations, contacts, calendar, documents, and attachments in your LifeDB, such as "When is dinner with Sam?" or "What did Riley send me about the lease?".

It works with Claude Code and Codex, the assistants that run in a terminal on your computer. It was tested with Claude Code 2.1.319 and Codex 0.166.0.

## Before You Start

You need three things:

- Claude Code or Codex, installed on your computer, and signed in to your account with its maker.
- A LifeDB account. Whoever runs your LifeDB invites you to it.
- Your LifeDB address. In LifeDB, open **Agents**. Under **Connect your assistant**, or **Connect another assistant**, choose **Show the steps** beside Claude Code or Codex, and copy the **Address of your LifeDB for assistants**. It starts with `https://` and ends in `/mcp`.

In each command below, replace `<your LifeDB address>` with that address, and keep the quotes around it. The plugin cannot check the address for you, so use only the one that LifeDB shows.

Before you connect, know that what the assistant reads from LifeDB becomes part of your conversation with it, which the assistant's maker processes. [Where Your Data Lives](#where-your-data-lives) says more.

## Install in Claude Code

Paste this into your terminal as one line:

```sh
claude plugin install lifedb --marketplace unbound-tools/lifedb-plugin --config lifedb_url="<your LifeDB address>" && claude mcp login plugin:lifedb:lifedb
```

Your browser opens on a LifeDB page. Check that the address in the browser's address bar is your LifeDB's, then sign in, check what the assistant may see, and choose **Allow**. Then start Claude Code and ask it a question about your messages or calendar.

If the browser does not open, copy the address that the command prints into your browser. If the command is not found or does not accept these options, update Claude Code first.

## Install in Codex

If you connected LifeDB to Codex before, the last command replaces that connection, which is named `lifedb`.

Paste this into your terminal as one line:

```sh
codex plugin marketplace add unbound-tools/lifedb-plugin && codex plugin add lifedb@lifedb && codex mcp add lifedb --url "<your LifeDB address>"
```

Your browser opens on a LifeDB page. Check that the address in the browser's address bar is your LifeDB's, then sign in, check what the assistant may see, and choose **Allow**. Then start Codex and ask it a question about your messages or calendar.

If the browser does not open, copy the address that the command prints into your browser. If signing in fails, or to sign in again later, run `codex mcp login lifedb`.

The plugin gives Codex the instructions for using LifeDB. The last command tells Codex your LifeDB address, because a Codex plugin cannot ask for it.

## What It Does

The plugin holds two things, and nothing else:

- Instructions that tell the assistant how to search your LifeDB, how to cite what it finds, and how to keep your data safe.
- The setting that connects the assistant to your LifeDB address.

When you ask a question, the assistant searches your LifeDB and answers with links to the items that it used, so you can open them in LifeDB.

The assistant only reads unless LifeDB gives it write access or a power to manage your sources or access, and you ask it for that change: to save a note, correct an item, say which person an address belongs to, or manage your sources and access. What it writes becomes part of your data in LifeDB, labelled with the assistant that wrote it.

## What It Never Does

- It changes nothing in your LifeDB unless two things are true: you gave this assistant write access, or the power to manage your sources or your access, in LifeDB, and you ask it for that change in your conversation. An assistant that signs in through your browser, as the steps above set up, gets read access only.
- With the power to manage sources or access, it can only narrow or take away access, start an import, or remove a source, whose imported data stays in LifeDB. Anything that gives more access or connects a source is only a proposal: nothing changes until you confirm it in LifeDB.
- It never removes an item from your LifeDB. No LifeDB tool that the assistant uses can do that.
- It never reads more than you allowed. LifeDB decides what each assistant may see, and the **Agents** page in LifeDB shows and changes it.
- It runs no program on your computer. The plugin is only the text files in this repository: no scripts, no programs, and no background tasks.
- It holds no password, key, or address of its own. You sign in through your browser, and your assistant keeps that sign-in on your computer.

## Where Your Data Lives

Your data is stored in your LifeDB. The plugin sends the assistant's questions only to the LifeDB address that you gave it.

What the assistant reads from LifeDB becomes part of your conversation with it. The assistant's maker processes that conversation, as it does everything else that you ask: Anthropic for Claude Code, and OpenAI for Codex. Their own terms and settings apply to it.

## Remove It

First, in LifeDB, open **Agents**, open the assistant, choose **Revoke**, and then **Revoke agent**. LifeDB ends its access within five minutes, unless whoever runs your LifeDB set another time, even on a computer that you no longer have. A file that the assistant is reading at that moment may take as long again to finish.

Then remove the plugin from your computer. From Claude Code, paste these lines:

```sh
claude mcp logout plugin:lifedb:lifedb
claude plugin uninstall lifedb@lifedb
claude plugin marketplace remove lifedb
```

From Codex, paste these lines:

```sh
codex mcp logout lifedb
codex mcp remove lifedb
codex plugin remove lifedb@lifedb
codex plugin marketplace remove lifedb
```

Revoking access does not remove what the assistant already read into your past conversations with it. Delete those conversations in the assistant if you want them gone.

## Security

To report a security problem, read [SECURITY.md](SECURITY.md).

## Licence

The plugin is available under the MIT licence, in [LICENSE](LICENSE). It comes without warranty.

Claude Code belongs to Anthropic, and Codex belongs to OpenAI. Neither makes nor endorses this plugin.
