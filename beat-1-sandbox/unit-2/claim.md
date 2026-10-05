Picking this up: `KeywordSearcher.index([])` is reported to raise a
`ZeroDivisionError` instead of handling an empty index cleanly.

I'll reproduce it locally first and post the environment, exact steps,
and observed output before attempting a fix. This is my first contribution
to this sandbox repo.