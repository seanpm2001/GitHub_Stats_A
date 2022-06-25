Run python3 --version
  python3 --version
  python3 generate_images.py
  shell: /usr/bin/bash -e {0}
  env:
    pythonLocation: /opt/hostedtoolcache/Python/3.8.12/x64
    LD_LIBRARY_PATH: /opt/hostedtoolcache/Python/3.8.12/x64/lib
    ACCESS_TOKEN: ***
    GITHUB_TOKEN: ***
    EXCLUDED: 
    EXCLUDED_LANGS: 
    EXCLUDE_FORKED_REPOS: true
Python 3.8.12
A path returned 202. Retrying...
Traceback (most recent call last):
  File "generate_images.py", line 136, in <module>
    asyncio.run(main())
  File "/opt/hostedtoolcache/Python/3.8.12/x64/lib/python3.8/asyncio/runners.py", line 44, in run
    return loop.run_until_complete(main)
  File "/opt/hostedtoolcache/Python/3.8.12/x64/lib/python3.8/asyncio/base_events.py", line 616, in run_until_complete
    return future.result()
  File "generate_images.py", line 132, in main
    await asyncio.gather(generate_languages(s), generate_overview(s))
  File "generate_images.py", line 42, in generate_overview
    changed = (await s.lines_changed)[0] + (await s.lines_changed)[1]
  File "/home/runner/work/GitHub_Stats_A/GitHub_Stats_A/github_stats.py", line 486, in lines_changed
    for repo in await self.repos:
RuntimeError: Set changed size during iteration
Error: Process completed with exit code 1.
