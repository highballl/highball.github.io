---
title: "Audio Visual Basic"
layout: posts
permalink: /categories/audio-visual/
categories:
  - audio-visual
tags:
  - Music
  - Audio-Visual
  - Max
#date: 2021-08-01T00:00:00
toc: true
---


`last update: 2021.08.10.Tue` 
# Audio Visual Basic
* 전자음악 및 사운드 아트 작업을 위한 공부용 문서
* 포트폴리오 아직 없음
* [연습 스케치 - Youtube](https://www.youtube.com/channel/UCJUV5_jyyUruSGFiBtUPktg)
<br >
<br >



### Audio-Visual Learning Experiences and Resources
* 2013-2014.  
Interactive Programming and other courses - [syllabus](http://art.snu.ac.kr/category/program-in-media-art/?cate=&catemenu=Courses&type=major)
* 2021.  
    1) Integrating MAX with Other Software and Languages by [Kadenze](https://www.kadenze.com/courses/programming-max-structuring-interactive-software-for-digital-arts)  
    2) Introduction to Live-Video Using Jitter by [Sabina Covarrubias](https://www.sabinacovarrubias.com/)



<br /><br /><br />
# Note
## Integrating MAX with Other Software and Languages by [Kadenze](https://www.kadenze.com/courses/programming-max-structuring-interactive-software-for-digital-arts)  
<br>

* 주로 max patch 위주의 실습을 했고, 패치에 주석을 달아두었으므로 따로 노트한 내용이 많이 없음.
<br><br>

## Session 1 : Introduction

### 1. Introduction: Scope of the Course(210406)

### 2. What can Max do?(210406)  

* Philippe Manoury - Musician, IRCAM, Univ. of California, San Diego  
* Miller Puckette - IRCAM programmer  
* Robert Henke - Ableton Live  
* Ableton Live는 PX18 Step Sequencer로 출발  
* The AlloSphere Research Facility   
Berna 2.0 - [Giorgio Sancristoforo Artist Sound-Designer Sound Art Sci-Art](https://www.giorgiosancristoforo.net/)  
* Damian Taylor - work with Bjork  
* Luke Dubois  
* Toni Dove

### 3. What is Max?(210406)

### 4. Getting Started: Building Blocks of Max(210406)
### 5. Building Our First Max Patch(210406)
### 6. Course Philosophy(210406)


<br><br><br>

## Session 2 : Fundamental Elements
### 1. Introduction: History of MAX(210406)  
- Alan Turing 1936 논문
- RTSKED 개념
- CNMAT github, wiki
    - 워크샵 자료도 많다
    * [CNMAT/CNMAT-MMJSS](https://github.com/CNMAT/CNMAT-MMJSS/wiki)
### _
2. Intro to MAX Programming(210406)
3. Immediate Gratification Elements: Audio GUI Object(210406)
4. Immediate Gratificatino Elements: Video(210406)
5. Visual Display and Control of MAX Data(210406)
6. Immediate Gratification Elements: MIDI(210406)
7. Objects in General(210406)
8. Customized QWERTY/Mouse Interaction and Pro(210406)
9. Outro(210406)

<br><br><br>

## Session 3 : What's Really Going on Inside Max

### 1. Logic and Scheduling of MSP's Signal Process(210413)
### 2. Digital Sampling & Sampling rate(210413)
### 3. The life of a gain~ object(210413)
### 4. The DAG of Signal Connections(210413)
- Undirected GRAPH (Computer Science)  
    → Edges and Nodes
- Directed GRAPH (Computer Science)  
    → 선에 화살표가 생기면 Directed GRAPH. 노드끼리 그냥 연결만 되어 있다면 Undirected.
- CYCLIC VERSUS ACYCLIC DIRECTED GRAPHS  
    → Topological sorting
### 5. Logic and Scheduling of MAX Events(210413)
- object-vs-message-boxes  
    stack over flow : task A→ task B 구조인데, A가 끝나야 B를 하는 구조이다. 그러나 무한히 루프가 반복된다면 이런 에러 메시지가 뜬다. 맥스는 C언어의 구조를 따른다. stacks and proceducre call. 
- Stack: First in, Last out. 
- This is psuedo code: qusi C language~
- The metro object:
    ```C
    onOffMethod(int zero_or_one){
	I.am_on = zero_or_one;
	if (this_object.is_on){ // Start metro
		// Output the first bang immediately
		outputABang();
		// Schedule future bangs
		LetMeKnowWhenTimeHasPassed(this_object.time_between_ticks);
        }
    }

    // Max calls this after (approximately) the requested time has elapsed
    TimeHasPassed(){
        If (this_object.is_on){ // Keep going
            // Output the next bang immediately
            outputABang();
            // Schedule future bangs
            LetMeKnowWhenTimeHasPassed(this_object.time_between_ticks);
        }
    }
    ```

- notein and noteout(이미지 누락, 대충 이진트리 구조 상상하면 됨)  
→ notein은 오른쪽에서 왼쪽으로, noteout도 오른쪽에서 왼쪽으로 데이터를 보낸다.  
→ noteout에서 빨간건 hot, 파란건 cool, 파란건 대기하겠다는 뜻. velocity와 channel이 그렇다.
- Trigger를 쓰면, 왼쪽 오른쪽 메시지 박스가 옮겨감에 상관없이 무조건 outlet에 연결된 순서대로 출력할 수 있다!

### 6. Right to Left Order(210413)
- 동일한 메시지 박스를 두어도 무조건 오른쪽에서 왼쪽으로 동작이 작동하므로, 나중에 입력 신호가 들어간 왼쪽 메시지의 명령이 실행되는 것처럼 보인다. 
- tree of connections.  
    = depth-first traversal

### 7. Arithmetic Operators(210413)
- 연산자 박스에서도 마찬가지. 왼쪽(빨강) 오른쪽(파랑), 오른쪽부터 왼쪽으로 데이터를 읽으며, 오른쪽 inlet에 들어오는 신호는 어떤 아웃풋을 트리거하지는 않는다. 단지 메모리에 저장할 뿐이다. in/outlet 의 색을 잘 기억해두자.
- 여기서도 trigger를 쓰면, 오른쪽 integer를 바꿔도 반응이 없던 결과물이 이제는 왼쪽 오른쪽 integer의 변화에 모두 동일하게 반응하게 된다. 그러니 trigger를 자주 쓰자!
- t b b  = trigger bang bang
- t b i  = trigger bang integer
- 연산자 쓸 때, 오→왼 순서를 잘 기억해야 한다. 특히 교환법칙이 성립하지 않는 뺄셈(!-, -)과 나눗셈인 경우에.
### 8. MAX objects for Control Flow & Scheduling(210414)
### 9. Example: A Simple Drum Machine(210414)
### 10. Logic and Scheduling of Jitter Events(210414)
- Events(Max) 
    * Key Issue or Questions : How fast can Max process message and can it keep up with incoming messages?
    * Ideal Situation : Process each message in zero time
    * Failure Mode : Delay message processing or scheduling while still dealing with earlier messages
- Signals(MSP)
    * Key Issue or Questions : What percent of my CPU does it cost to execute the entire signal processing graph?
    * Ideal Situation : Lots of signal processing with low CPU % usage.
    * Failure Mode : Audio glitch (hardware needs samples before MSP finishes cmputing them)
- Video/Matrices(Jitter)
    * Key Issue or Questions : What frame rate can I get?
    * Ideal Situation : Lots of image processing at high resolution with a high video frame rate
    * Failure Mode : Slower and slower frame rate
### 11. MAX's Data Types in Depth(210414)
- int  
    32bit integer - 1bit : sign bit: positive negative number, 31 numbers  
    so the higher number is: 2147483647  
    counter object에서는 이 다음 숫자가 0으로 돌아간다  
    다른 경우는 그냥 integer object의 경우 음수로 취급해서 계산한다.  
- float  
    부분적으로 64비트 넘버를 지원하고 보통은 32비트를 지원한다.  
    → Mantissa(23bits)  
    → Exponent(8bits)   
### 12. Outro(210414)

<br><br><br>

## Session 4 : Getting Mathematical: Arithmetic, Logic, Matrices

1. Intro: Elementry Arithmetic in Max, MSP, and Jitter(210416)
2. Linear Interpolation in Max, MSP, and Jitter(210416)
3. Clipping in Max, MSP, and Jitter(210416)
4. Random Numbers and Noise(210419)
5. Logarithmic Scales Approximating Human Perception(210419)
6. Random Melodies on Linear vs Log Frequency Scale(210419)
7. Boolean Logic (Ture/False)(210419)
8. Dividing the Octave in Twelve(210419)
9. The Coll Object(210419)
10. Musical Scales, Keys, Octave Equivalence(210419)
11. Example: Playing Scales from Coll with Amplitude(210419)
12. Repeating a Scale at the Octave(210419)
13. The Harmonic Series(210419)
14. Octaves, Half Steps, Cents, and Frequency Ratios(210420)
15. Different Kinds of Musical Fifths and Thirds(210420)
16. Outro(210420)

<br><br><br>



## Session 5 : Structuring Non-Trivial Patches

1. Intro(210422)
2. Wobble Bass Example(210422)
3. Techno~ and Finding a Need for Encapsulation(210422)
4. Subpatchers and Encapsulation(210422)
5. Sync Signals and Getting a Bang on Every Loop(210422)
6. Programming techno~ with Max Messages(210422)
7. Bpatchers: Subpatchers you can see inside(210422)
8. Philosophies of Encapsulation, Naming, and Development(210422)
9. Presets and Snpahosts(210422)
10. List Processing with Message Boxes(210422)
11. List-Processing Objects in Max: Pack, Route and Friends(210422)
12. The Sprintf Object(210422)
13. List Processing with the ZL Object(s)(210423)
14. Note Lists, Round Robin Scheduling and Routing by Data(210423)
15. Recording and Playing back Sound in Realtime with Buffer(210423)
16. Global and Local Variables with Value and PV(210423)
17. Using Coll(Collection) as a List of Notes(210423)
18. Storing Data with the Dict("Dictionary") Object(210423)
19. Send and Receive(210423)
20. Outro(210423)


<br><br><br>


## Session 6 : Abstractions, Files, and How Max Works

1. Where Max Keeps and Looks for Files(the Search Path)(210428)
2. Kinds of Files to Put in Your Search Path(210428)
3. How to Read and Write the Kinds of Files Max Typically Uses(210428)
4. Abstractions: Philosophy and Mechanism(210428)  
* abstractions는 서브패쳐와는 다르게 하나의 명령어처럼 작동하기 때문에 하나의 패러미터가 바뀌면 전역에 영향을 주게 된다.
5. AV Sine Synth Part 1: Synthesizing Sine Wave Sounds(210428)
6. AV Sine Synth Part 2: Graphically Drawing a Sine Wave(210428)
7. AV Sine Synth Part 3: Interface and Abstraction for Drawing Squiggles and Clearing(210429)
8. AV Sine Synth Part 4: Defining a Mapping from Blip Parameters to Squiggle Parameters(210429)
9. AV Sine Synth Part 5: Controlling it with a Generative Process(210429)
10. AV Sine Synth Part 6: Overlapping Notes and Polyphony(210429)
11. Review: How Max Works(How the Interpreter Runs Your Patch(210429)
12. Exceptions to Max's Normal Evaluation Rules(210429)
13. How MSP Works: I/O and Signal Vectors(210429)
14. Jitter Works Just Like Max(210429)
15. Scheduling in Max, MSP and Jitter(210429)
* defer, deferlow, qlim, qmetro
16. Outro(210429)

<br><br><br>


## Session 7 : Data Types

1. Intro to the the Max Type Conversion Table(210505)
2. Type Conversions 1: From Bang(210505)
3. Type Conversions 2: From Integer(210505)
4. Type Conversions 3 : From Float(210506)
5. Type Conversions 4 : From Symbol(210506)
6. Type Conversions 5 : From List(210506)
7. Type Conversions 6 : From Signal(210506)
8. Type Conversions 7 : From Matrix(210506)
9. Matrix Processing(210506)
10. Displaying Matrices with jit.window(210506)
11. RGB and HSV Color Spaces(210506)
12. Video Analysis with Centroid Tracking(210506)
13. Directly Converting Pixel Values to Audio(210506)
14. Rastograms(210506)

<br><br><br>

## Session8 : Interactivity

1. Intro
2. Examining the Messages a MIDI Controller Outputs(210518)
3. Abstracting a MIDI Controller(210518)
4. Mapping a MIDI Device to Control a Patch(210518)
5. Virtually Representing a MIDI Device with a Graphical Interface, Part 1(210518-19)
6. Virtually Representing a MIDI Device with a Graphical Interface, Part 2(210519)
7. Switching to a Different MIDI Device with the Power of Abstraction(210520)
8. Open Sound Control(210520)
9. Making Your Own Wifi Network and Other Advanced Networking Topics(210520)
10. Sending OSC from a Phone(210520)
11. Connecting Arduino with Max(210520)
12. Glue Code: Controlling an Arduino from a Phone via Max
13. Glue Code 2: Searching the Web with a MIDI Pad Controller
14. Interfacing Max with Modular Synthesizers
15. Interfacing Max with HID Devices
16. Sample-Synchronous Processing 1: Motivation and Simple Examples(210527)
17. Sample-Synchronous Processing 2: Programming Techniques(210527)
18. Sample-Synchronous Processing 3: Boolean Signal Logic(210527)
19. Outro
<br><br><br>


## Session9 : Max programming paradigms

1. Session Intro and List of Topics(210603)
2. Abstractions as Objects: Naming, Help Patch, Inlets and Outlets
3. Abstractions as Objects: Arguments
4. Abstractions as Objects: Allowing Multiple Instance
5. Abstractions as Objects: Coordinating Multiple Instances with Gating and Delegation
6. Abstractions as Objects: Coordinating Muliple Instances with Poly~
7. Using "Midinote" with Poly~ if You Don't Know the Duration in Advance
8. Constraint-Style Programming with "Set"
9. Non-Realtime Processing with Uzi
10. Recording a Movie in Realtime and Non-Realtime
11. Using Max to Write, Save and Load Max Patches
12. Example: Ensemble Feedback Instruments
13. Example: Ensemble Feedback Instruments(Continued)
14. Global Transport and Time Value Syntax
15. 3D Graphics with OpenGL
16. Top-Down and Bottom-Up Programming
17. Outro