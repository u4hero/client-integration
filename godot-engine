var _game_pause_callback = JavaScript.create_callback(self, "_game_pause")

func event_listener():
	var window = JavaScript.get_interface("window")
	window.addEventListener("GamePause", _game_pause_callback)

func _game_pause(args):
	var console = JavaScript.get_interface("console")
	console.log("PAUSE GAME")
	
func question_trigger():
	var window = JavaScript.get_interface("window")
	var event = JavaScript.create_object("CustomEvent", "TriggerQuestion")
	window.dispatchEvent(event)
