---
name: book-a-call
description: Find open times on a WhenNOT booking page and book, move or cancel a call there, or list the user's own booking pages and upcoming bookings. Use when the user gives a whennot.com/m/ link and wants a time, asks to book, reschedule or cancel a call on WhenNOT, or asks what calls they have coming up.
---

# Book a call

Book one of the open times of a WhenNOT booking page as the user, and manage the bookings the user
made or hosts.

## Rules for every step

- `book_time`, `reschedule_booking` and `cancel_booking` send email and change calendars. Say the
  time, in the user's time zone, and wait for a yes before you call them.
- `cancel_booking` cannot be undone. Name the booking (who, when) in your question.
- Offer only times that `find_open_times` returned. Send `startAt` exactly as the tool gave it.
- The user can cancel or move only bookings they made or host. If the tool refuses, say so.
- Take booking ids from `list_bookings`. Never guess one.

## Workflow

### Book

1. **Find the page.** Use the link the user gave (`https://whennot.com/m/…`). For the user's own
   pages, call `list_booking_pages`.
2. **Find open times.** Call `find_open_times` with the page. It shows up to 7 days from `from`
   (default today), in the user's time zone. For "next week" send the Monday as `from`. When
   nothing is open, look at the next 7 days once, then tell the user.
3. **Choose.** List a few times that fit what the user asked for and let the user pick one.
4. **Questions of the page.** When the answer of `find_open_times` lists `questions`, ask the user
   for the answers and send them in `answers`, keyed by the question label. `notes` holds anything
   else for the host.
5. **Book.** After a yes, call `book_time`. Confirm the time. The host and the user both get a
   calendar invite by email.

### Move

1. Call `list_bookings` and find the booking. Use `cursor` for the next page.
2. **A booking the user made:** call `find_open_times` for the same page, let the user pick, then
   call `reschedule_booking` with `startAt`.
3. **A booking on a page the user hosts:** the host cannot move it alone. Call
   `reschedule_booking` with `proposals` (1 to 5 new starts) and an optional `note`. The guest gets
   an email and picks. The booking keeps its time until then: say so.

### Cancel

1. Call `list_bookings` and find the booking.
2. Ask "Cancel the call with … on …?" After a yes, call `cancel_booking`. Both sides get an email
   and the calendar event is removed.
