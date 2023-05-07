Download Link: https://assignmentchef.com/product/solved-me227-assignment-7-navigating-the-hairpin-corner
<br>
In this assignment, we will add longitudinal and lateral weight transfer to our bicycle model and see how handling at the limits of tire friction can be influenced by load transfer. We’ll consider load transfer caused by braking, acceleration, and suspension roll stiffness.

We’ll explore these concepts while using a new tire model, the Pacejka Magic Formula (MF). The MF tire model is a semi-empirical model that has stood as a reference point in tire modelling since its introduction in the late 1980s.

Download the source code zip folder hw7.zip from Canvas. In it you’ll find the code you’ll need for Problems 1, 3 and 4.

<h1>Instructions</h1>

This and following homework assignments will be submitted using two different tools, Gradescope and MATLAB Grader. Throughout the assignment, each prompt will be marked with either <strong>Gradescope </strong>or <strong>MATLAB Grader </strong>to make it clear where you should be submitting the answer to that problem. MATLAB Grader questions will also be shown in <strong>Blue </strong>to make them easy to see.

All written portions must be turned in through Gradescope. See the Piazza post on homework guidelines for more instructions on the different homework resources available to you. Whatever format you decide to use, please <strong>BOX </strong>all of your final answers.

Some problems will make use of the MATLAB Grader suite discussed in class. These problems are available directly from Canvas by clicking on each individual question. You are allowed to submit code to MATLAB Grader as many times as you want before the due date without penalty. In this way you can be sure each function or script passes all of the assesments that go along with it before moving on to the next problem. We encourage you to write your own test cases as well to ensure your code is working as expected.

Additionally, some problems will make use of <strong>MATLAB Online </strong>or a normal MATLAB desktop installation. For these problems we will give you most of the source code needed for the problem. See our Piazza post for more information about how to setup MATLAB Online.

When writing functions and running simulations, use the set of parameters given to you for Niki. These will be available in each MATLAB Grader problem where they are appropriate. The values of these paramters for Niki are also given in Appendix A and B at the end of this document.

1

<h1>Exploring the Magic Formula</h1>

In this assignment, we will move away from the Modified Fiala Tire Model that we’ve been using and explore the Pacejka Magic Formula tire model. The Modified Fiala Model is a good, simple way to represent tire force generation, and we can derive it nicely from physical observations. However, the Magic Formula is able to represent some more complex tire characteristics that often interest manufacturers and racing teams so it has evolved into the industry standard since its inception in the late 1980s. In its more complex form, we can use it to calculate <em>F<sub>x </sub></em>and <em>F<sub>y </sub></em>using longitudinal slip, lateral slip, tire load, friction coefficient and wheel camber. We’ve decided to introduce it here to give you exposure to what you may see in industry, not because the Fiala Model is flawed. Quite the opposite, The Fiala Model does a very good job of representing our tire dynamics given its simplicity.

If you’d like to read more about the Magic Formula, we recommend checking out Pacejka’s <em>Tire and Vehicle</em>

<em>Dynamics </em><a href="https://www.sciencedirect.com/science/article/pii/B9780080970165000048">(</a><a href="https://www.sciencedirect.com/science/article/pii/B9780080970165000048">https://www.sciencedirect.com/science/article/pii/B9780080970165000048</a><a href="https://www.sciencedirect.com/science/article/pii/B9780080970165000048">)</a>. For the context of this homework, we will use a simplified Magic Formula of the form <em>F<sub>y </sub></em>= <em>f</em>(<em>µ,F<sub>z</sub>,F<sub>x</sub>,α</em>) to calculate lateral force analogously to the simplified Fiala Model.

Let’s compare <em>F<sub>yf </sub></em>and <em>F<sub>yr </sub></em>from the two models:

If you’re looking at the plots and saying, ”these two models look pretty much the same,” that is the point. We’ve simply substituted one mathematical representation for our tires for another, both tuned for the same set of tires. We can notice some difference between the curves in the slip range between the linear and saturated regions, and that is where these models tend to differ slightly with the Magic Formula more closely matching recorded data.

The Teaching Team has taken care of implementation of the Magic Formula in MF_tire.m. Nonetheless, we do recommend checking out the magic behind the Magic Formula in some of Pacejka’s papers.

<h1>Problem 1 – How to Race Through the Hairpin Corner</h1>

In this problem we’ll gain some intuition about how we’ll manuever through the hairpin corner described below:

hairpin_corner.mat contains path information about a 180 degree hairpin turn in the same format we used in the project. The path consists of a straight of 40m, a clothoid segment 100m long, a 75m radius arc segment with a length of 135m, another 100m clothoid, and finally another 40m straight.

The file also contains the desired acceleration and velocity profiles for the corner. These were calculated using a simple friction circle model, so they aren’t necessarily what the vehicle will be able to achieve.

Download and unzip the hw7.zip file from Canvas. Open up the viewPathAndSpeedProfile.m script in the Problem1/ directory. Run this script in MATLAB Online or MATLAB Desktop to plot the path and speed profile described in the problem info. You don’t need to add or modify any code here, you just need the plots to answer the following question.

<h2>Question 1.A – Understanding the Hairpin Corner (Gradescope)</h2>

Refer to the plots generated in viewPathAndSpeedProfile.m and answer the following questions:

<ol>

 <li>At what speed does the car travel on the constant radius arc?</li>

 <li>What lateral acceleration (in g’s) does this correspond to?</li>

 <li>At what level of acceleration (in g’s) is the car braking on the initial straight?</li>

 <li>At what level of acceleration (in g’s) is the car accelerating on the final straight?</li>

</ol>

<em>Answer the questions based on the plots of the path and speed profile for the hairpin corner.</em>

<h1>Problem 2 – Calculating Weight Transfer and Effective Friction Coefficient</h1>

When modeling vehicle behavior at the limits, there are three new phenomena we need to account for which we have not simulated previously. These are:

<ul>

 <li>Longitudinal load transfer</li>

 <li>Lateral load transfer</li>

 <li>Friction as a function of tire normal load</li>

</ul>

In class we derived equations for lateral and longitudinal weight transfer. To combine them, simply calculate the longitudinal weight transfer from the longitudinal acceleration and the lateral weight transfer from the lateral accleration and sum the effects on each wheel.

Be careful when calculating the lateral load transfer term proportional to the roll center height. Think about what the proper weight or normal force is to use for this term. If you understand the static roll model and its underlying assumptions, there is a clear answer here.

<h2>Question 2.A – Calculating Weight Transfer (MATLAB Grader)</h2>

Follow the prompts on MATLAB Grader to create a function to calculate the normal load on each tire and the body roll angle given longitudinal and lateral accelerations.

<h2>Question 2.B – Calculating Effective Friction (MATLAB Grader)</h2>

Follow the prompts on MATLAB Grader to create a function to calculate the effective friction available at each axle.

You should use the following relationship for friction coefficient as a function of normal load to get the friction at each tire:

<em>µ </em>= 1<em>.</em>25 − (4<em>.</em>0 × 10<sup>−5</sup>)<em>F<sub>z</sub></em>

You can then find the effective friction coefficient for each axle by taking a weighted sum of the left and right tires:

<h3>Question 2.C – How Does Weight Transfer Affect Friction (Gradescope)</h3>

In the ”Run Function” section of the MATLAB Grader assignment <strong>Question 2.B</strong>, there are three combinations of roll stiffness as listed in Table 7.1 below.

<table width="368">

 <tbody>

  <tr>

   <td width="106"><strong>Combination</strong></td>

   <td width="157"><strong>Parameter</strong></td>

   <td width="105"><strong>Value</strong></td>

  </tr>

  <tr>

   <td width="106">Combination A</td>

   <td width="157">Front Roll Stiffness <em>K<sub>φf</sub></em></td>

   <td width="105">40,000 Nm<em>/</em>rad</td>

  </tr>

  <tr>

   <td width="106"> </td>

   <td width="157">Rear Roll Stiffness <em>K<sub>φr</sub></em></td>

   <td width="105">80,000 Nm<em>/</em>rad</td>

  </tr>

  <tr>

   <td width="106">Combination B</td>

   <td width="157">Front Roll Stiffness <em>K<sub>φf</sub></em></td>

   <td width="105">90,000 Nm<em>/</em>rad</td>

  </tr>

  <tr>

   <td width="106"> </td>

   <td width="157">Rear Roll Stiffness <em>K<sub>φr</sub></em></td>

   <td width="105">30,000 Nm<em>/</em>rad</td>

  </tr>

  <tr>

   <td width="106">Combination C</td>

   <td width="157">Front Roll Stiffness <em>K<sub>φf</sub></em></td>

   <td width="105">70,000 Nm<em>/</em>rad</td>

  </tr>

  <tr>

   <td width="106"> </td>

   <td width="157">Rear Roll Stiffness <em>K<sub>φr</sub></em></td>

   <td width="105">50,000 Nm<em>/</em>rad</td>

  </tr>

 </tbody>

</table>

Table 7.1: Roll Stiffness Combinations

A quick way to gain intuition about the effects of roll stiffness is to see how the car behaves at a constant lateral acceleration. Here we’ve set up a scenario where the vehicle is cornering at 0.9g. Run your function and answer the following questions for each combination of roll stiffnesses:

<ol>

 <li>What is the roll angle at 0.9g lateral acceleration?</li>

 <li>How much load is on each tire when the vehicle is cornering at 0.9g?</li>

 <li>What are the front and rear friction coefficients when the vehicle is cornering at 0.9g?</li>

</ol>

<em>Answer the questions about the vehicle’s behavior for each combination of roll stiffnesses.</em>

<h1>Problem 3 – Simulating and Tuning Vehicle Setup</h1>

Through previous homeworks, you’ve built up a nonlinear vehicle simulator to analyze vehicle behavior and design autonomous controllers. As you saw in the project, this simulator captures a good amount of detail of the vehicle’s real behavior, but not all of it. In this question we will add one more level of complexity by accounting for weight transfer and roll effects. We have supplied all of the code you need for this Problem in the Problem3/ directory included in the hw7.zip file on Canvas.

In this problem we will simulate Niki racing through the hairpin corner you saw in <strong>Problem 1</strong>. It is important to note that Niki is front wheel drive; this will frame your analysis of Niki’s behavior through the manuever. The simulation will run for 14 seconds. By keeping the simulation time the same, we can compare the value of <em>s </em>reached when the simulation ends. A higher value of <em>s </em>means we made greater progress through the corner, and consequently did a better job navigating the corner.

The simulator included here is essentially your nonlinear vehicle simulator with the weight transfer and effective friction calculation functions you wrote in <strong>Problem 2</strong>. This is all conducted using the MF tire model, not the modified Fiala Model we’ve used in previous assignments.

When asked you will just need to comment/uncomment different roll stiffness and brake distribution combinations in the simulator.m script and run the simulation to see how a different setup affects you performance through the corner. You will then need to implement aerodynamic effects in aero_effects.m from a splitter and wing that we’ll mount on Niki.

<h2>Question 3.A – Benchmarking Our Setup (MATLAB Online / Gradescope)</h2>

Begin with a brake distribution of 64%/36% between the front and rear axle, and roll stiffness Combination A (from Table 7.1). If we want to be able to follow the path within 2m of the desired path, how are we doing at this point? Which tire saturates at the start of the turn? Is this limit understeer or limit oversteer behavior? What evidence do we have that this is the case?

<em>Run the simulation and answer the questions about the vehicle’s behavior. Include the tire force plots.</em>

<h2>Question 3.B – Tuning Roll Stiffness (MATLAB Online / Gradescope)</h2>

Let’s try to address our handling problems by adjusting roll stiffness. Combination A has the majority of the stiffness on the rear axle which is not common for passenger vehicles. Let’s try the simulation again with Combination B to see if we do any better.

Did this correct the problem we saw with Combination A? Did it create another issue, and if so, what was it? Did we make better progress through the corner (in other words, is our final distance along the path greater at the end of our 14 second simulation time)?

<em>Run the simulation and answer the questions about the vehicle’s behavior. Include the tire force plots.</em>

<h2>Question 3.C – Tuning Roll Stiffness – Continued (MATLAB Online / Gradescope)</h2>

Finally, try roll stiffness Combination C in the simulation. This combination is closest to what you would see on the production vehicle. Describe what is happening to the car through the corner and why that is different from Combination A or Combination B. Which combination allows us to cover the greatest distance in our 14 second simulation period? What is the maximum absolute lateral error?

<em>Run the simulation and answer the questions about the vehicle’s behavior. Include the tire force plots.</em>

<h2>Question 3.D – Tuning Brake Proportioning (MATLAB Online / Gradescope)</h2>

Now that we have an idea of how to best setup our roll stiffness from <strong>Question 3.C</strong>, let’s take a look at changing the brake setup. Set up the simulation with roll stiffness Combination C.

Change the brake proportioning to 36%/64% between the front and rear axle. Describe what is happening to the vehicle with this setup, and what problems we’ve created by reversing the brake proportioning.

<em>NOTE: You will get warnings about tire forces when running this setup. Why do these warnings crop up? This should give you a hint as to what is happening.</em>

<em>Run the simulation and answer the questions about the vehicle’s behavior. Include the tire force plots.</em>

<h1>Problem 4 – Tricking Out Niki</h1>

We’ve decided that Niki needs an upgrade. You are to mount a full aerodynamic-enhancing body kit on Niki. Let’s envision Niki looking something like this:

<em>https://www.rtheorymotorsports.com/shop/mk7-golf-tsigtir-rear-wing-kit</em>

We added a front splitter and a rear wing. The additional downforce for each of these can be modelled as:

<em>C<sub>LA </sub></em>is the coefficient of lift for that wing. <em>ρ </em>is the air density.

This may look familiar to one of the feedforward components of the longitudinal controller you implemented in the project. And in fact, we can use the same equation with different coefficients (where <em>C<sub>DA </sub></em>is the coefficient of drag) to model the additional drag caused by the new wings:

<h2>Question 4.A – Adding Aerodynamics (MATLAB Online / Gradescope)</h2>

Modify aero_effects.m to implement the added downforce and drag from the wing. We can assume that the front wing aero forces act at the center of the front wheel and that the rear wing aero forces act at a distance veh.hRwing directly above the rear wheel. We can also assume that the front wing acts equally on the left and right front wheels and that the rear wing acts equally on the left and right rear wheels. Here is a free body diagram of the GTI with the forces we added with the two wings.

<a href="https://www.vw.com/en/models/golf-gti.html">https://www.vw.com/en/models/golf-gti.html</a>

<em>Note: The drag on the rear wing will have an impact on the downforce on the front axle. Be sure to account for this.</em>

Restore Niki’s brake distribution to the original 64/36. Now, simulate the same curve as in the previous problem. How does the distance covered compare to Question 3C? How does the maximum lateral error compare to 3C? Plot the front and rear tire forces. Provide the plots and describe what is happening. Does it make sense to add an aero kit to Niki?

<em>Run the simulation and answer the questions about the vehicle’s behavior. Was it a good idea to upgrade Niki? Include the tire force plots.</em>

<h1>Appendix A – Vehicle Parameters</h1>

<table width="502">

 <tbody>

  <tr>

   <td width="116"><strong>Variable Name</strong></td>

   <td width="60"><strong>Value</strong></td>

   <td width="53"><strong>Units</strong></td>

   <td width="273"><strong>Description</strong></td>

  </tr>

  <tr>

   <td width="116">veh.m</td>

   <td width="60">1926.2</td>

   <td width="53">kg</td>

   <td width="273">Mass (Includes 4 passengers)</td>

  </tr>

  <tr>

   <td width="116">veh.Iz</td>

   <td width="60">2763.49</td>

   <td width="53">kgm<sup>2</sup></td>

   <td width="273">Yaw Moment of Inertia</td>

  </tr>

  <tr>

   <td width="116">veh.a</td>

   <td width="60">1.264</td>

   <td width="53">m</td>

   <td width="273">Distance from Center of Mass to Front Axle</td>

  </tr>

  <tr>

   <td width="116">veh.b</td>

   <td width="60">1.367</td>

   <td width="53">m</td>

   <td width="273">Distance from Center of Mass to Rear Axle</td>

  </tr>

  <tr>

   <td width="116">veh.L</td>

   <td width="60">2.631</td>

   <td width="53">m</td>

   <td width="273">Wheelbase</td>

  </tr>

  <tr>

   <td width="116">veh.Wf</td>

   <td width="60">9817.9</td>

   <td width="53">N</td>

   <td width="273">Static front axle weight</td>

  </tr>

  <tr>

   <td width="116">veh.Wr</td>

   <td width="60">9078.1</td>

   <td width="53">N</td>

   <td width="273">Static rear axle weight</td>

  </tr>

 </tbody>

</table>

Table 7.2: Vehicle Parameters and Values

<h1>Appendix B – Tire Parameters</h1>

<h2>Linear Tire Model</h2>

<table width="391">

 <tbody>

  <tr>

   <td width="116"><strong>Variable Name</strong></td>

   <td width="60"><strong>Value</strong></td>

   <td width="53"><strong>Units</strong></td>

   <td width="162"><strong>Description</strong></td>

  </tr>

  <tr>

   <td width="116">f_tire.ca_lin</td>

   <td width="60">80,000</td>

   <td width="53">N<em>/</em>rad</td>

   <td width="162">Front Cornering Stiffness</td>

  </tr>

  <tr>

   <td width="116">r_tire.ca_lin</td>

   <td width="60">120,000</td>

   <td width="53">N<em>/</em>rad</td>

   <td width="162">Rear Cornering Stiffness</td>

  </tr>

 </tbody>

</table>

Table 7.3: Linear Tire Model Parameters

<h1>Appendix C – Aero Parameters</h1>

<table width="500">

 <tbody>

  <tr>

   <td width="116"><strong>Variable Name</strong></td>

   <td width="54"><strong>Value</strong></td>

   <td width="53"><strong>Units</strong></td>

   <td width="277"><strong>Description</strong></td>

  </tr>

  <tr>

   <td width="116">veh.hRwing</td>

   <td width="54">1.5480</td>

   <td width="53">m</td>

   <td width="277">Distance from rear wheel center to rear wing</td>

  </tr>

  <tr>

   <td width="116">veh.cdAf</td>

   <td width="54">0.0180</td>

   <td width="53">m2</td>

   <td width="277">Drag coefficient of the front wing</td>

  </tr>

  <tr>

   <td width="116">veh.cdAr</td>

   <td width="54">0.0315</td>

   <td width="53">m2</td>

   <td width="277">Drag coefficient of rear wing</td>

  </tr>

  <tr>

   <td width="116">veh.clAf</td>

   <td width="54">0.1080</td>

   <td width="53">m2</td>

   <td width="277">Lift coefficient of front wing</td>

  </tr>

  <tr>

   <td width="116">veh.clAr</td>

   <td width="54">0.2331</td>

   <td width="53">m2</td>

   <td width="277">Lift coefficient of rear wing</td>

  </tr>

 </tbody>

</table>

Table 7.4: Aero Parameters and Values