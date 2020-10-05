# Labs Book Club

Each week, we meet to discuss some technical aspect of a chapter of a book or a blog post or a video. To provide some structure around our discussion, we ask a member of the team to lead.

The book club leader's responsibilities are the following:

1. Read the chapter/blog post or watch the video
2. Take notes and/or come prepared with discussion questions
3. Make sure there's a leader for the following week

You don't need to be an expert in the chapter to lead book club. Just bring your own curiosity and excitement.

This repo holds our group notes for the books we've been reading. Notes aren't required, but they a) serve as a great jumping point for discussion and b) remind us of what we've learned.

## Adding Notes

### For a video or blog post

Add a director to the `./mini-topics` directory. Name it `#{YYYY-MM-DD}-name-of-talk-or-blog`. Add a `readme.md` file inside this dir. If you want to add pictures, put them somewhere in this director (perhaps a nested `images` directory?). Make sure to put your name and a link to the source material at the top of your readme file!

Update the [mini-topics index](./mini-topics/readme.md) with a link  to your new  notes. 

### For a Book

Each book has its own directory. If you want to add notes for a given book, create a Markdown file in the directory and name it with the convention `"#{ chapter/section number }-#{ subject summary }.md`.

Please use integers and dots to describe the chapter (like a software version number) to keep notes alphabetized sequentially alongside the book. For example, `3.1-collecting-inputs.md`. Also, a lot of technical books are already organized like this!
