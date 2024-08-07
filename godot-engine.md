```
var _pause_game_callback = JavaScript.create_callback(self, "_pause_game")
var _resume_game_callback = JavaScript.create_callback(self, "_resume_game")
var _mute_all_sound_callback = JavaScript.create_callback(self, "_mute_all_sound")
var _un_mute_all_sound_callback = JavaScript.create_callback(self, "_un_mute_all_sound")

func event_listener():
	var window = JavaScript.get_interface("window")
	window.addEventListener("PauseGame", _pause_game_callback)
	window.addEventListener("ResumeGame", _resume_game_callback)
	window.addEventListener("MuteAllSound", _mute_all_sound_callback)
	window.addEventListener("UnMuteAllSound", _un_mute_all_sound_callback)

func _pause_game(args):
	var console = JavaScript.get_interface("console")
	get_tree().paused = true
	console.log("PAUSE GAME")

func _resume_game(args):
	var console = JavaScript.get_interface("console")
	get_tree().paused = false
	console.log("RESUME GAME")
	
func _mute_all_sound(args):
	var console = JavaScript.get_interface("console")
	var bus_idx = AudioServer.get_bus_index("Master")
	AudioServer.set_bus_mute(bus_idx, true)
	console.log("MUTE SOUND")
	
func _un_mute_all_sound(args):
	var console = JavaScript.get_interface("console")
	var bus_idx = AudioServer.get_bus_index("Master")
	AudioServer.set_bus_mute(bus_idx, false)
	console.log("UNMUTE SOUND")
	
func question_trigger():
	var window = JavaScript.get_interface("window")
	var event = JavaScript.create_object("CustomEvent", "TriggerQuestion")
	window.dispatchEvent(event)
```
