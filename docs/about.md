# About Auto-Building Jupyter Notebooks and RMarkdown Files: Our CI Pipeline

When we originally created earthdatascience.org, we never imagined that it would
balloon into a resource being used by thousands of people around the world! Ok
so maybe we did dream that would happen, but we never knew it would happen
so quickly. As our lessons became more popular and our user base grew (we are
now up to >56,000 unique users a month) we realized that maintaining this content
was a challenge. We wanted an easier way to update lessons.

Previously we had been updating this manually. This was fine when only one or
two of our team was contributing. It became increasingly challenging when we wanted
different people to help us update content.

We built this pipeline to make it easier for anyone to contribute content to
earthdatascience.org. Through this pipeline, anyone who has access to our private
repo, can submit a new lesson to our website. This repo could easily be public if you
don't need to hide homework answers! Rather than worrying about building the lessons,
the user can submit a pr with a `Rmarkdown` or `Python` notebook. That file gets built,
and images produced by the file are created and moved to our website repo.
If the build fails, the user can identify why it failed and then submit a change.

The build also includes a cron job that is set to run weekly. This is an ongoing
test that the lessons build. We hope that other people find this build useful.
It needs a lot of cleanup. As such, all contributions are welcome!
