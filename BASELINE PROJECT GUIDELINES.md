
#############################################################################################
#                                                                                           # 
#                                 Second DiCOVA Challenge                                   #
#                            Diagnosing COVID-19 Using Acoustics                            #
#                                 Baseline system software			            #
#                             http://dicovachallenge.github.io/                             #
#                                                                                           #  
#############################################################################################

---------
1. About:
---------

The DiCOVA Special Session/Challenge is designed to find scientific and engineering insights
into diagnosing COVID-19 using acoustics. As part of the challenge an acoustic dataset gathered
from COVID-19 positive and non-COVID-19 individuals is provided for analysis. Here we provide
a baseline system software which you can use to get started on the challenge. This is a system
written with a python back-end and a shell front-end, and follows object oriented programming
paradigm. It is composed of the following parts:
- Feature extraction
- Model initialization
- Model training, and exporting
- Validation data classification
- Performance computation

The modularized structure, organization into seprate python files, and intergration of the
pipeline using shell allows easy scalability and modification as per user needs. As an example,
we have presented a baseline system with
- Features: Log-Mel-Spectrogram (64 dimensional + delta + delta-delta)
- Classifier: Bidirectional Long Short-Term Memory (BLSTM) 

This is a simple model to get you started on the challenge. We will like you to build your own
model and beat the performance of the baseline system as best as you can. Below we describe the
directory structure of the content inside the software.

-----------------------
2. Directory structure:
-----------------------
.
├── LICENSE.md
├── README
├── conf
│   ├── feature_config
│   ├── train_config
│   └── model_config
├── local
│   ├── dataset.py
│   ├── feature_extraction.py
│   ├── infer.py
│   ├── models.py
│   ├── score_fusion.py
│   ├── scoring.py
│   ├── train.py
│   └── utils.py
├── parse_options.sh
├── REQUIREMENTS.txt
├── run.sh
└── prepare_data.sh

----------------------
3. Directory contents:
----------------------

- conf/
	-- feature_config			[ Configuration file used by the feature extraction module ]
	-- model_config				[ Configuration file used by the neural net architecture ]
	-- train_config				[ Configuration file used by the training script ]

- run.sh					[ Master (shell) script to run the codes ]
- parse_options.sh				[ Facilitates inputing command-line arguments to run.sh (borrowed
                                		from Kaldi, note the license details inside it)]
-local/
	- dataset.py				[ torch dataset class ]
	- feature_extraction.py			[ Extract features requires feature_config, and the FLAC audio file list]
	- infer.py               		[ Inference: forward pass through the trained model to generate
                                		scores as probalities]
	- models.py                 		[ Model definition: contains model details]
	- score_fusion.py           		[ Score fusion ]
	- scoring.py                    	[ Performance: computes false positives, true positives, etc.,
                                		from ground truth labels and the system scores ]
	- train.py                  		[ Training : uses models.py, dataset.py, utils.py ]
	- utils.py                 		[ utilities ]

- REQUIREMENTS.txt              		[ Contains a list of dependencies to run the baseline system ]

--------------
4. How to run:
--------------
- Create "DICOVA" directory
- Place "Second_DiCOVA_Challenge_Dev_Data_Release" inside "DICOVA" directory
- Place the "Second_DiCOVA_Baseline" inside "DICOVA" directory
- Open shell terminal (Linux/MAC), navigate to "Second_DiCOVA_Baseline"
- Create a soft link to "Second_DiCOVA_Challenge_Dev_Data_Release" by typing the following and hit enter:
$ ln -s ../Second_DiCOVA_Challenge_Dev_Data_Release/ Dataset
- Type the following and hit enter: 
$ ./run.sh (In run.sh, make "stage=0" when you run first time. You can make "stage=1" next time onwards.)
Note: In case you are not familiar with shell, you can run each python file contained inside Second_DiCOVA_Baseline
seprately too after understanding the code flow inside run.sh.

--------------------
4. Baseline results:
--------------------
-----------------------------------------------------------------------------------------
[ Sensitivity is computed at specificity >=95% ] 
[ Average metrics across the five validation folds are reported below ] 
-----------------------------------------------------------------------------------------
Track			|	AUC (std)	|		Sensitivity (std)	|
-----------------------------------------------------------------------------------------
Breathing		|	77.24 (3.71)	|		27.98 (7.18)		|
-----------------------------------------------------------------------------------------
Cough			|	75.22 (2.28)	|		30.74 (8.40)		|
-----------------------------------------------------------------------------------------
Speech			|	80.18 (3.92)	|		40.06 (9.65)		|
-----------------------------------------------------------------------------------------
Fusion			|	81.68 (3.03)	|		45.26 (6.66)		|
-----------------------------------------------------------------------------------------

* depending on the version of python packages in your system, the performance may be little different in
the decimal places.

--------------
7. Contact Us:
--------------

Please reach out to dicova.challenge@gmail.com or the organizers for any queries.


--------------
8. Organizers:
--------------

Team DiCOVA
- Sriram Ganapathy | Assistant Professor, IISc, Bangalore
- Prasanta Kumar Ghosh | Associate Professor, IISc, Bangalore
- Neeraj Kumar Sharma | CV Raman Postdoctoral Researcher, IISc, Bangalore
- Srikanth Raj Chetupalli | Postdoctoral Researcher, IISc, Bangalore
#############################################################################################
