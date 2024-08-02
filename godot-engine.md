```
var _pause_game_callback = JavaScript.create_callback(self, "_pause_game")
var _resume_game_callback = JavaScript.create_callback(self, "_resume_game")

func event_listener():
	var window = JavaScript.get_interface("window")
	window.addEventListener("PauseGame", _pause_game_callback)
	window.addEventListener("ResumeGame", _resume_game_callback)

func _pause_game(args):
	var console = JavaScript.get_interface("console")
	get_tree().paused = true
	console.log("PAUSE GAME")

func _resume_game(args):
	var console = JavaScript.get_interface("console")
	get_tree().paused = false
	console.log("RESUME GAME")
	
func question_trigger():
	var window = JavaScript.get_interface("window")
	var event = JavaScript.create_object("CustomEvent", "TriggerQuestion")
	window.dispatchEvent(event)
```
