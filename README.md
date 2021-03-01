# Callable Bond Valuation 

A callable bond is a bond in which the issuer has the right to call the bond at specified times from the investor for a specified price. At each callable date prior to the bond maturity, the issuer may recall the bond from its investor by returning the investor’s money. The underlying bonds can be fixed rate bonds or floating rate bonds. A callable bond can therefore be considered a vanilla underlying bond with an embedded Bermudan style option. Callable bonds protect issuers. Therefore, a callable bond normally pays the investor a higher coupon than a non-callable bond. 

For issuers, callable bonds allow them to reduce interest costs at a future date should rate decrease. For investors, callable bonds allow them to earn a higher interest rate of return until the bonds are called off. If interest rates have declined since the issuer first issues the bond, the issuer is like to call its current bond and reissues it at a lower coupon. Callable bonds protect issuers. Therefore, a callable bond normally pays investors a higher coupon than a non-callable bond. This presentation gives an overview of callable bond and valuation model.



	Callable Bond Definition
	A callable bond is a bond in which the issuer has the right to call the bond at specified times (callable dates) from the investor for a specified price (call price).
	At each callable date that is prior to the bond maturity, the issuer may recall the bond from its investors by returning the investors’ money.
	The underlying bonds can be fixed rate bonds or floating rate bonds.
	A callable bond can therefore be considered a vanilla underlying bond with an embedded Bermudan style option that gives the issuer the right to buy the bond back.
	Comparing to a normal bond, a callable bond is a higher cost to the issuer and an uncertainty to the investors.


	The Advantage of Callable Bonds
	For issuers, callable bonds allow them to reduce interest costs at a future date should rate decrease.
	For investors, callable bonds allow them to earn a higher interest rate of return until the bonds are called off.
	If interest rates have declined since the issuer first issues the bond, the issuer is like to call its current bond and reissues it at a lower coupon.
	Callable bonds protect issuers. Therefore, a callable bond normally pays investors a higher coupon than a non-callable bond. 


	Callable Bond Payoffs
	At the bond maturity T, the payoff of a callable bond is given by


V_c (T)={■(F+C                 if not called@〖min⁡(P〗_c,F+C)        if called)┤
where 
F – the principal or face value; 
C – the coupon; 
P_c – the call price; 
T -  the maturity date;
min (x, y) – the minimum of x and y

	The payoff of the callable bond at any call date T_i can be expressed as

 (3)

V_c (T_i )={■(¯V_(T_i )                                  if not called@min⁡(P_c,¯V_(T_i ) )                        if called)┤
where 	
¯V_(T_i ) – continuation value at T_i
P_c – the call price; 
T_i -  the i-th call date;
min (x, y) – the minimum of x and y


	Model Selection Criteria
	Given the valuation complexity of a callable bond (e.g., embedded Bermudan option), there is no closed form solution. Therefore, we need to select an interest rate term structure model and a numeric solution to price the callable bond.
	The selection of interest rate term structure models
	Popular IR term structure models: 
Hull-White, Linear Gaussian Model (LGM), Quadratic Gaussian Model (QGM), Heath Jarrow Morton (HJM), Libor Market Model (LMM).
	HJM and LMM are too complex.
	Hull-White is inaccurate for computing sensitivities.
	Therefore, we choose either LGM or QGM.
	 The selection of numeric approaches
	After selecting a term structure model, we need to choose a numeric approach to approximate the underlying stochastic process of the model.
	Commonly used numeric approaches are tree, partial differential equation (PDE), lattice, and Monte Carlo simulation.
	Tree and Monte Carlo are notorious for inaccuracy in sensitivity calculation.
	Therefore, we choose either PDE or lattice.
	We decide to use LGM plus lattice. 

	LGM Model
	The dynamics
dX(t)=α(t)dW
	Where X is the single state variable; W is the Wiener process.
	The numeraire is given by
N(t,X)=(H(t)X+0.5H^2 (t)ζ(t))/D(t)
	The zero coupon bond price is
B(t,X;T)=D(T)exp(-H(t)X-0.5H^2 (t)ζ(t))

	LGM Assumption
	The LGM model is mathematically equivalent to the Hull-White model but offers
	Significant improvements in calibration stability and accuracy.
	More accurate and stable in sensitivity calculation.
	The state variable is normally distributed under the appropriate measure.
	The LGM model has only one stochastic driver (one-factor), thus changes in rates are perfected correlated.

	LGM calibration
	Match today’s curve
At time t, X(0)=0 and H(0)=0. Thus Z(0,0;T)=D(T). In other words, the LGM automatically fits today’s discount curve.
	Select a group of market swaptions.
	Solve parameters by minimizing the relative error between the market swaption prices and the LGM model swaption prices.

	Valuation Implementation
	Calibrate the LGM model.
	Create the lattice based on the LGM: the grid range should cover at least 3 standard deviations.
	Find the underlying swap value at each final note.
	Conduct backward induction process iteratively rolling back from final dates until reaching the valuation date.
	Compare exercise values with intrinsic values at each exercise date.
	The value at the valuation date is the price of the callable bond.

	A real world example

Bond specification	Callable schedule
Buy Sell	Buy	Call Price	Notification Date
Calendar	NYC	100	1/26/2015
Coupon Type	Fixed	100	7/25/2018
Currency	USD		
First Coupon Date	7/30/2013		
Interest Accrual Date	1/30/2013		
Issue Date	1/30/2013		
Last Coupon Date	1/30/2018		
Maturity Date	7/30/2018		
Settlement Lag	1		
Face Value	100		
Pay Receive	Receive		
Day Count	dc30360		
Payment Frequency	6		
Coupon	0.012		


You can find more details at
https://finpricing.com/faq.html

