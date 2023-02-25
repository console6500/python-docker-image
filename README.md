# Steps for For Python API
- Create repo
- add files from exercise files
- click actions tab
- scroll down to Continuous Integration section
- selection python app
- build job includes 5 steps
	- checkout
	- python set up for 3.10
	- install dependencies
		- pip install flake8 and pytest
		- will also install requirements if requirements.txt is present
	- lint with flake8
	- test with pytest
- add `workflow_dispatch` to the triggers
- add the following under "runs_on"...
```
    permissions:
      checks: write
```
- change pytest call to: `pytest --verbose --junit-xml=junit.xml`

-- add the following job at the end:
```
    - name: Publish Test Report
      uses: mikepenz/action-junit-report@v3
      if: success() || failure() # always run even if the previous step fails
      with:
        report_paths: '**/junit.xml'
        detailed_summary: true
        include_passed: true
```
- commit new file directly to main branch 
- go to actions tab
- select create python-app.yml job
- wait for build to complete; open build
- checkout and set up steps pass
- expand "install dependencies"
- requirements file was present so it was used to install deps
- close "install dependencies"
- expand "lint with flake8"
- comment on results
- close "lint with flake8"
- expand "test with pytest"
- comment on tests passing and amount of time needed (less than 1s)
- close "test with pytest"
-


## Notes
- Mention the need to include ${{ secrets.GITHUB_TOKEN }} for actions that provide features (like the junit reporter)
- Mention [assigning permissions to a job](https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs)
	- [Permissions](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token)
- Mention using conditionals in CI to keep workflow going
	- `if: success() || failure()`




