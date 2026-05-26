
Link to your GitHub Classroom hw5 repository / branch:
https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-Rimen611 
Link to .cursorignore: 
https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/blob/main/.cursorignore
Links to AGENTS.md , .cursor/rules/rails-conventions.mdc , and
.cursor/rules/security.mdc
- https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/blob/main/AGENTS.md
- https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/blob/main/.cursor/rules/rails-conventions.mdc
- https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/blob/main/.cursor/rules/security.mdc 


## Part 3: 
### Ask Mode:
Prompt: Where in this codebase is the todo done checkbox behavior currently implemented? Cite the exact files and line numbers. Do not propose changes.
Response:
- `app/views/todos/_form.html.erb`, lines 24–27: checkbox input for `done`
- `app/views/todos/new.html.erb`, line 5: renders the form partial
- `app/views/todos/edit.html.erb`, line 5: renders the form partial
- `app/controllers/todos_controller.rb`, lines 74–76: permits `:done` in `todo_params`
- `app/controllers/todos_controller.rb`, lines 23–24: creates todo with `todo_params`
- `app/controllers/todos_controller.rb`, lines 38–40: updates todo with `todo_params`
- `app/views/todos/_todo.html.erb`, lines 12–15: displays done as text
- `db/migrate/20260417190631_add_done_to_todos.rb`, lines 1–4: adds `done` boolean column

### Plan Mode:
Prompt:
I want to change the todo done behavior so that overdue todos cannot be marked done. Propose a plan as a numbered list of changes, including files to edit, new tests to add, and any migration. Do not write code.
Response: 
1. No migration needed because `done` and `due_date` already exist.
2. Add model-level logic in `app/models/todo.rb`
   - Add an `overdue?` method
   - Add validation preventing overdue todos from being marked done
   - Allow overdue todos to still be edited if `done` remains false
3. Update `app/views/todos/_form.html.erb`
   - Disable or hide the done checkbox for overdue todos
   - Show a message explaining why
4. Update fixtures in `test/fixtures/todos.yml`
5. Add model tests in `test/models/todo_test.rb`
   - overdue todo cannot be done
   - future todo can be done
   - no due date can be done
6. Add controller tests in `test/controllers/todos_controller_test.rb`
7. Run `bin/rails test`

Edits:
- Kept the no-migration decision because `done` and `due_date` already exist.
- Kept model-level validation as the main enforcement point.
- Kept model and controller tests.
- Removed optional system/UI tests.

### Agent mode:
Prompt:
Implement only the `overdue?` method in `app/models/todo.rb`. Do not modify views, controllers, tests, routes, or migrations. 

Commit link: https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/commit/329c1f7f0e14aa836fd5743746f3dad7936593fa


Bad -> good prompt rewrite:
Bad prompt: fix the bug in todos

Good prompt:

Context:
- app/views/todos/_form.html.erb
- app/controllers/todos_controller.rb
- test/controllers/todos_controller_test.rb

Task:
Add tests for the todo done checkbox behavior.

Expected vs actual:
Expected: The app should have tests verifying that the `done` checkbox value is saved correctly when creating and updating todos.
Actual: The current app has no tests covering the done checkbox behavior.

Constraints:
- Only modify test files if possible.
- Do not add new gems.
- Follow Rails testing conventions.

Done when:
- Creating a todo with `done: true` passes a test.
- Updating a todo with `done: true` passes a test.
- `bin/rails test` passes successfully.

## Part 4: 

Turbo Streams let a Rails application update only specific parts of a page instead of reloading the entire page. The server sends instructions that tell the browser to perform actions such as append, replace, update, or remove elements from the page. This allows changes to appear as needed without a full page refresh.

Cursor said that Turbo Streams support actions such as append, prepend, replace, update, remove, before, and after. I checked the Turbo Streams handbook and confirmed that these actions are listed there. I found that Turbo Streams use these actions to update specific parts of a page without requiring a full page reload.


Pull Request: https://github.com/NU-CS-Software-Studio-Spring-26/todo_app/pull/12 
