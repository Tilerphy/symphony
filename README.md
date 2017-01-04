
# symphony
scheduler Stepper

# Idea

A way to reduce the cost of calculating nexttime of all jobs.

Before:

1. Use SQL, may be "SELECT JobId, JobName, JobNextTime, JobAction, IsFinished from Jobs where JobNextTime < 123456789 and JobNextTime > 12345", to find all jobs those need to run EVERY STEP.

2. Then ask worker to execute the jobs.

Now:

1. Use SQL too, but cache the job into a STEPs Calendar.

For example: 30 second per Step:

0 : Job1, Job2, Job3, Job4...

30: Job5, Job10 ...

60: Job6, Job7 ...

90:

120: Job8...


when the STEP on an index, then execute the jobs in Calendar, No need to run SQL *EVERY Time*.

2. BUT!, the Jobs Updating in DATABASE must be synced to the Calendar.

However, Use the Memory to exchange CPU (Maybe include Network IO/DataBase Memory/DataBase Space).
