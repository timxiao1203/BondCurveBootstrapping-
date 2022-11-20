# Government Bond Curve Bootstrapping Procedure

We discuss a method for bootstrapping a set of zero rates from an input set of US government money market securities and bonds. The government bond bootstrapping procedure requires to input a set of financial instruments, of the type below, sorted by order of increasing time to maturity:

	Short term money market instruments (i.e., USD T-Bills with maturity not more than one year),
	Medium to long term “on the run” US government bonds,
	Medium to long term “off the run” US government bonds.

First of all, we need to have a bond valuation model to calculate bond price or bond yield (see https://finpricing.com/lib/FiZeroBond.html)

To determine discount factors at times intermediate to control points, we can apply a particular interpolation technique. There are three available:

	LINEAR
	LOG_LINEAR
	TIME_WEIGHTED_LINEAR

The LINEAR scheme interpolates zero rates linearly between successive control points on the zero curve; that is, if r(t_1) and r(t_2) are bootstrapped continuously compounded zero rates at successive control points, then
	r(t)⥂=r(t_1)+(r(t_2)-r(t_1))  (t-t_1)/(t_2-t_1 )    where t_1≤t≤t_2. 	(1)

The LOG_LINEAR scheme interpolates linearly between ln⁡r (t_1) and ln⁡r (t_2), that is,
ln⁡r (t)⥂=ln⁡r (t_1)+(ln⁡r (t_2)-ln⁡r (t_1))  (t-t_1)/(t_2-t_1 )   or   
	r(t)=r(t_1)((r(t_2))/(r(t_1)))^(((t-t_1)/(t_2-t_1 )) ).	(2)

The TIME_WEIGHTED_LINEAR scheme interpolates between r(t_1)t_1 and r(t_2)t_2,
	r(t)=1/t (r(t_1)t_1+(r(t_2)t_2-r(t_1)t_1)(t-t_1)/(t_2-t_1 )),	(3)

where t>0and t_1≤t≤t_2. Since t2>t1, the TIME_WEIGHTED_LINEAR scheme weights rate information farther in the future more heavily than rate information in the near future.

Government Bond Bootstrapping proceeds in two phases. The first phase uses short term instruments, which typically mature in one year or less. Consider, for example, a US government money market instrument with 

	D calendar days between settlement date, S, and maturity date, S+D, and 
	with a corresponding simple forward interest rate r.

Then
	(_S^)d f_(S+D)=1/(1+r D/360),	(4)

where the “360” factor arises from the ACT/360 market convention used for US government money market instruments yields, is the forward price at the date, S, of a zero coupon bond with maturity date, S+D, and unit face value. 

Let a bond have the cash flow, c_i, at date, t_i t_i, for i=1,...,n. Our Benchmark applies a Newton iterative scheme to solve
	((_0^)d f_S ) P_d=∑_(i=1)^n▒〖c_i ((_0^)d f_(t_i ) ) 〗,

for the unknown zero rate at t_n where S is the settlement date. Here we use the “Time Weighted Linear” interpolation scheme to determine intermediate discount rates.



