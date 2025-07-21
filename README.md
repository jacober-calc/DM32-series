———————————————————————————————————————————
jacober-calc’s
Astrodynamics Statefile Program
Version 1.0 (20 July 2025)
———————————————————————————————————————————

CONTENTS

1 ………………………	Licence and Use
	1.1 ……    	Licence
	1.2 ……     	Use
2 ………………………	Download and Install
	2.1 ……		Download
	2.2 ……		Install
3 ………………………	Program Index
	3.1 ……       	General Mechanics of the State File
	3.2 ……		Initiator Programs
	3.3 ……		Sub-routines
	3.4 ……		Solar System Constants
4 ………………………	Instructions
	4.1 ……		Solar System Constants Routine
	4.2 ……		Constants Sub-routine
	4.3 ……		Initiator Programs
	4.4 ……		Sample Problem
5 ………………………	List of Constants
6 ………………………	Notes on Program
	6.1 ……		SI Units
	6.2 ……		Assumptions
	6.3 ……		Calculation Accuracy
	6.4 ……		Variables Used
7 ………………………	Dedication

SECTION 1 - Licence and Use

	1.1 - Licence

	GNU GENERAL PUBLIC LICENSE - Version 3, 29 June 2007

	1.2 - Use

	Use of this state file is subject to the terms in the Licence. Please do not share file on any archives or hosts without permission from the author. Please go to Github 			repository to report issues/bugs and collaborate on future developments (jacober-calc’s DM32-series GitHub).
	
 All calculations are based on theoretical CIRCULAR orbits which will vary from real life orbits based on the real eccentricity of any actual orbits.

SECTION 2 - Download and Install

	2.1 - Download

	State file is available for download at the Github repository or via the official SwissMicros forum (https://forum.swissmicros.com/).

	Compressed file contains .dm32 format state file, this readme, and instructional screenshots.

	2.2 - Install

	Activate the USB Disk on your DM32 calculator and open the drive. After decompressing the file, simply move the Astrodynamics.dm32 file to your state file folder. When the transfer is complete. Unmount the DM32 calculator disk drive. Open the state file menu (F4) and select Load (F2). The state file Astrodynamics should appear near the top. Select it and press ENTER to load the state file.

SECTION 3 - Program Index

	3.1 - General Mechanics of the State File	

	The state file contains a total of 8 individually labelled routines. Some of these are main programs that are selected 	based on the variable input by the user. Others are sub-routines that conduct routine operations within the main programs. One is a sub-routine specifically for the final display and another is a large program that stores solar 			system data in a host of indirect global registers.

	While a deep knowledge of these system is not required at all to use the state file, if you wish to make changes this section will be helpful in understanding the mechanics of the state file as a whole.

	The state file has the programs listed in the following order:
 
			(1)	LBL O	DISPLAY SUB-ROUTINE
			(2)	LBL Z	CONSTANTS SUB-ROUTINE
			(3)	LBL H	HEIGHT INITIATOR PROGRAM
			(4)	LBL V	VELOCITY INITIATOR PROGRAM
			(5)	LBL P	PERIOD INITIATOR PROGRAM
			(6)	LBL D	SIDEREAL DAY INITIATOR PROGRAM
			(7)	LBL C	CIRCUMFERENCE INITIATOR PROGRAM
			(8)	LBL A	SOLAR SYSTEM CONSTANTS ROUTINE

	3.2 - Initiator Programs

	LBL H (height)
	User inputs height (from the surface) of the satellite.
	SI: 	km

	LBL V (velocity)
	User inputs velocity of the satellite.
	SI: 	m/s

	LBL P (period)
	User inputs period of the satellite orbit.
	SI: 	min

 	LBL D (sidereal days)
	User inputs number of sidereal days of the satellite orbit.
	SI: 	dec

	LBL C (circumference)
	User inputs circumference of the satellite orbit.
	SI: 	km

	3.3 - Subroutes

	LBL Z (constant sub-routine)
	Prompts user for standard gravitational parameter (INPUT G) and radius (INPUT R) of main body. For each prompts it loads the constants for the MOON in the z-register and for Earth in the y-register. The x-register is left open for user input. Subroutine runs via XEQ within each Initiator Program. User can recall values stored from running LBL A 			for all planets in the solar system, the MOON, and the SUN.
	SI: 	radius (R), m; stand. gravitation parameter (G), m3s2

	LBL O (display sub-routine)
	Displays final results at the end of each Initiator Program. Recalls height (H) displaying finally on the t-register, velocity (V) displaying finally in the z-register, circumference (C) displaying finally in the y-register, period (P) displaying finally in the x-register, and VIEW sidereal days (D). All Initiator Programs end with 	LBL O via GTO.
	SI: 	height (H), km; velocity (V), m/s; circumference (C), km; period (P), min; sidereal days (D), dec

	3.4 - Solar System Constants

	LBL A (system constants routine)
	Stores constants for the standard gravitational parameter (G), radius (R), and distance from the SUN (H) as well as AU, sidereal days in a solar year and radius of Earth in indirect global extended registers. See SECTION 5 for a full listing of these constants.
	
SECTION 4 - Instructions

4.1 - Solar System Constants Routine

	Before starting any calculators it is recommended that the user run LBL A. This program will STO useful constants of standard gravitational parameters, radiuses and distance from the sun of planets in the solar system. See SECTION 5 for a complete list and location of each constant.

4.2 - Constants Sub-routine

	Although not the first step in running calculators by the user, the Constants Sub-routine (LBL Z) will run for each Initiator Program. The user will be promoted to input the standard gravitational parameter (m3 s2) of the main body as well as the radius (m). For each value the calculator will display the relevant constant for the MOON (z-register) and EARTH (y-register), and the x-register will be blank. If you desire to use the EARTH you can simply click R(down) for the register to move 	down one and load the value in the input field. You can click this twice for the MOON. For all other values you can 	input yourself or use the useful constants stored in the indirect registers via LBL A. Simply type the relevant indirect register, STO i and then RCL (i) to load the constant in the input field. See SECTION 5 for a complete list and location of each constant.

4.3 - Initiator Programs

	This is the first step to begin any calculation. The user inputs the relevant single-variable (either height, velocity, period, sidereal days or circumference) and runs a specific program based on the information provided. For example:

	If the user desires to calculate orbital data based on orbit height above the Earth the user will input the height	(in km) and press XEQ H to run the height Initiator 				Program. This will commence the routine and the next prompt will be from the Constants Sub-routine, asking for the standard gravitational parameter and radius of the main body (see SECTION 4.2 above). Once the user inputs the relevant constant information, the routine will continue and will end with LBL O will will display the orbital information on the four-line display along with a VIEW of the sidereal day value.

	If the user desires orbital information based on velocity, the same procedure is followed only the user will initiate the calculations by selected XEQ V. The Constants Sub-routine will run again prompting for the G and R constants.

4.4 - Sample Problem

	You wish to calculate orbital data for the ISS which orbits approximately 407 km above the surface of the Earth.

	Optional pre-step: Run L BL A subroutine to load constants into indirect registers. We are using Earth for this calculation which is pre-loaded in the Constant Sub-routine, but it is a good habit to have these constants pre-loaded so the user can calculate orbital information for any planetary body in the Solar System.

	Step 1: enter 407 in the x-register.
	Step 2: run LBL H Initiator Program by selecting XEQ H.
	
	Step 3: input Earth G constant by pressing R(Down) and R/S.

	Step 4: input Earth R constant by pressing R(Down) and R/S.

	Step 5: view data, press R/S to close sidereal days VIEW.

	The user can run another calculation using any of the input 	variables and Initiator Programs and the calculator will remember the constants input for G and R (until the memory is cleared for those variables). This allows the user to make many calculations with the same main body without having to input the data again (the user will still be prompted but the valid value will be stored in the input field). This is particularly useful when the constants held in indirect registers are used.

Section 5 - List of Constants

	The follow section details the constants that are stored in indirect registers via use of the LBL A routine. This only needs to be run periodically to ensure the data is still stored properly. Variables are accessible via any state file and are stored across the device. 

	See the DM32 User Manual for how to recall these variables which is especially useful when inputting the G and R constants for any orbit around a main body. There is also a 	series of constants stored for planetary distance from the SUN and the distance of the MOON from the EARTH.

	There is some method to the madness here. Universal constants are stored in the -100 series, all other planetary constants are stored in the -900 series. Each 			planet corresponds to it’s position relative to the SUN	(the SUN is 0) in the Solar System (so EARTH will end in 3, 	MARS in 4, JUPITER in 5, etc). PLUTO is not represented in this list, the 9 is reserved for the MOON. All standard gravitational parameters are -90X, radiuses are -91X and distances from the SUN (or from the EARTH in the case of the MOON) are -92X.

SECTION 6 - Notes on Program

6.1 - SI Units

	Standard SI units are used throughout this program. All distances are presented and inputted in km (converted and calculated as m in each routine). All speeds are in v/s and 	are calculated in each routine in the same. All times are presented in minutes but are calculated in the routines using seconds. Sidereal days are calculated by the second 			and converted to decimal form for presentation.

6.2 - Assumptions

	All calculations are based on a theoretical circular orbit. Variance from real life orbits are based on the eccentricity of the particular orbit. For EARTH orbit 				calculations the error is within +/- 0.5% for all values owing to the low eccentricity of the real life orbit.

6.3 - Calculation Accuracy

	All calculations are done in SI using metres for distance, m/s for speed and seconds for time. Conversions are done to 	make the data more palatable for user consumption within each sub-routine. While the calculator will truncate numbers for display purposes, all digits are used in calculations, leveraging the 32-bit precision of the DM32 			handheld calculator.

6.4 - Variables Used

	This program uses the following variables:

	i (if needed) - recalling indirect register for constants
	C - circumference in km
	D - sidereal days in decimal form
	G - standard gravitational parameter
	H - orbital height from surface of main body (km)
	P - period in minutes
	R - radius in meters
	V - velocity in m/s

Section 7 - Dedication

	This humble state file and the tremendous (and often tedious) work that went into making it possible is dedicated to the vision and efforts of the thousands of unnamed individuals who contributed to the GEMINI and APOLLO programs culminating in landing man on the moon in the 20th century. Much of what we nerd out on and enjoy today by way of technology can be traced to their work and effort to put a man on the moon and we remain forever in their debt.
