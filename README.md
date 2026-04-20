It is now time to visualize the online processing for which you're provided a skeleton framework (find it attached. To run it, ensure you have `python-socketio`, `uvicorn`, and `aiohttp`, along with `numpy` and `scipy` installed, see `requirements.txt. To start the data provisioning and frontend 'server', use the arguments `--microarray_path`, `--eeg_data_path`, and `--stimuli_path` pointing to the respective directories. It serves data to any 'worker' requesting it (given at least a pair number) and receives processing results in a structured format. An example of this is given in `processing.py. The 'worker' `processing.py` receives a `data_event` and puts a small chunk of data (only a few samples in time, (500 = 16000 / update_rate) assuming an update_rate of 32) into queues that can be flushed based on the window sizes of the different processing tasks. If you decide to stick with this setup, most of the processing happens in the Processor class. It is also here, where most of your code will go. It provides three result queues for later pickup. Any intermediate results are pushed there, and picked up by `processing.py` to send back to the 'server'. If a frontend is connected (accessible via localhost:8000), it will visualize the results. Make sure, however, that the update_rate and window_size are consistent over 'server' and 'worker' scripts. For audio output, connect the AudioContext first, then decide which audio to play. For all provided codes, you are free to change whatever you want as long as you don't infringe on the integrity of the ground truth.
 
As a reference, here's the mapping of pairs to eeg files that use the two stimuli of the pair: pair_subject_mapping_15 = 
'pair1': [8, 13, 6, 12, 5, 19, 4, 2, 3, 25, 18, 15, 26, 7, 24, 10, 11, 16], 
'pair2': [28, 31, 27, 29, 30], 
'pair3': [32, 33, 35, 34, 36], 
'pair4': [38, 37, 41, 42, 40, 39], 
'pair5': [45, 46, 44, 43], 
'pair6': [47, 48], 
'pair7': [55, 49, 52, 56, 53, 54, 51], 
'pair8': [59, 57, 62, 61, 58, 60], 
'pair9': [69, 66, 63, 64, 68, 71, 70, 65, 67], 
'pair10': [73, 76, 75, 72, 74, 78], 
'pair11': [73, 76, 75, 72, 74, 78], 
'pair12': [73, 76, 75, 72, 74, 78], 
'pair13': [79, 82, 84, 80, 83, 85], 
'pair14': [79, 82, 84, 80, 83, 85], 
'pair15': [79, 82, 84, 81, 80, 83, 85], 
For the attention prediction you can use the beamformed signals, however, a ground truth signal is provided. Also, collect evaluation metrics to discuss in the report.

The mapping between each audio pair and the corresponding EEG subjects can be found in issp_data.py


