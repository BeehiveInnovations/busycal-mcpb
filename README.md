# BusyCal for Claude

BusyCal for Claude lets Claude work with the calendars, events, and tasks in BusyCal on your Mac. You can ask Claude what's on your schedule or when you're free, and have it add, change, or remove events and tasks for you.

## Requirements

- A Mac with BusyCal installed from busymac.com or Setapp
- Claude Code or Claude Desktop on the same Mac

## Install

Install BusyCal from the Claude plugin directory.

To use BusyCal as a Claude Desktop extension instead, download the `.mcpb` file from the latest release in this repository and open it in Claude Desktop.

## What Claude can do

- List your BusyCal accounts, calendars, and calendar sets
- Search events, tasks, journals, graphics, and stickies by keyword, date range, or calendar
- Read the items selected in BusyCal, or one item by its ID
- Check when you're free or busy, and find the next free time
- Create events, tasks, and journals, including from everyday text such as "Lunch with Sam on Friday at noon"
- Create a task calendar
- Update, move, reschedule, duplicate, complete, reopen, and delete events and tasks
- Show an event or task in BusyCal

Tools that only read your data are marked as read-only. The tools that delete events and tasks are marked as destructive.

## What the plugin runs

The plugin starts one local MCP server, `server/BusyCalMCPBridge`. This is a native macOS program built by Beehive Innovations, signed with the Busy Apps FZE Developer ID, and notarized by Apple. Claude starts it with no arguments and talks to it through standard input and output. The program reads its tool definitions from `server/tool-metadata.json`.

## What the plugin connects to

The program connects only to BusyCal on the same Mac. It sends each request to BusyCal through a local socket file in BusyCal's app group folder: `~/Library/Group Containers/N4RA379GBW.com.busymac.busycal3`, or `~/Library/Group Containers/N4RA379GBW.com.busymac.busycal-setapp` for the Setapp version.

If BusyCal isn't running, the program removes any socket file left over from an earlier session, opens BusyCal in the background with the `--mcp-service` option, and waits for it to accept requests.

The program makes no network connections. It doesn't download files, install software, or send data to Beehive Innovations or anyone else. Apart from opening BusyCal, it doesn't run other programs.

## What the plugin sends to Claude

The program returns BusyCal's answers to Claude. These results contain the calendar data that a request asks for, such as titles, dates, locations, notes, and calendar names. Claude receives them as part of your conversation.

When Claude creates, changes, or deletes an event or task, BusyCal saves the change and syncs it with your calendar accounts, the same way it syncs changes you make in BusyCal.

## Source code

This repository contains the compiled program only. The BusyCal source code is private.

## Privacy and support

- Privacy policy: https://www.busymac.com/privacy
- Documentation: https://www.busymac.com/docs/busycal/70624-mcp
- BusyCal: https://www.busymac.com/busycal/
