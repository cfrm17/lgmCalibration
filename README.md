# LGM Calibration Approach


The Gaussian HJM interest rate (IR) term structure model, also called the Linear Gaussian Model (LGM), is used to pricing some IR structured products. To keep it being consistent with the IR option market, the model needs to be calibrated to the IR European swaption market.

The traditional calibration routine in the model works only in a domestic market, in other words, it is not applicable to cases with funding in a foreign currency. The new calibration routine corrects the old one in LGM European swaption price calculation when a basis spread adjusted zero curve is applied for a non-reference currency.

To the purpose of calibration, one needs the pricing formula of European swaptions under the LGM. Under the LGM, underlying swaps of swaptions are expressed as affine linear portfolios of zero bonds.

In traditional calibration, the (forward) Libor rates and discount factors in the underlying swap are calculated off the single domestic, such as JPY, yield (or zero rate) curve and the swaption is treated as an option on an affine linear portfolio of zero (or discount) bonds to which the Jamshidian zero bond option formula is applied.

In the cases when swap funding is from a reference foreign currency, such as USD or EUR, the Libor rates on the floating leg of the underlying swap are now forecasted off a zero curve which is called the forecasting curve, and the discounting factors for payments on both legs are now calculated from a zero curve which is called the discounting curve. Thus, for the floating leg, an adjustment for the spread between the forecasting curve and discounting curve implied Libor rates is required.

We provide highlights of the LGM European swaption pricing approach. The key step is to mathematically formulate the value of the underlying IR swap when a pair of basis spread adjusted zero curves are applied for a non-reference currency, such as JPY or AUD.

Let us consider IR swaps in the domestic currency. Instead of considering pricing the swaps in the IR domestic market, we shall derive an evaluation model in a dual-currency IR market. Clearly, the model will trivially reduce to one in the IR domestic market. Pricing the domestic IR swaps in the dual currency market, we need a pair of so-called (cross currency) basis-spread-adjusted zero curves, named forecasting and discounting curves. 

The two basis-spread-adjusted curves are simultaneously generated based on arbitrage-free in both the domestic swap market and the cross-currency basis swap market. As it is shown below, we will take (basis spread adjusted) discount bond price processes as our fundamental dynamics. With the IR term structure LGM, all bond relative prices have log-normal distributions. We set the current time to be zero and t > 0 to be a generic time point and some notations.

In the domestic IR swap market, we denote the zero bond price by pdom(t, T). In that market, the domestic zero bond price is used for both discounting and forecasting. It is assumed that any index rate is defined by a function of finitely many zero bonds. An domestic index (forward) rate corresponding to a single accrual period [t0, t1] at a time t, denoted as L(t; t0, t1) which is usually called a Libor rate, is defined as

 

where αL is the day-count fraction (DCF) of the index accrual period with a given accrual day-count convention (DCC).


In the dual-currency IR market, if the domestic currency is not the reference currency, then a pair of bonds, named the (basis-spread-adjusted) forecasting and discounting (zero) bonds, are needed. Discount factors and forward rates in the domestic currency may not be obtained directly from the domestic zero bond price pdom(t, T). 

Instead, to avoid arbitrage in the domestic swap market and the cross-currency basis swap market, discount factor must be calculated by using the discounting bond price, denoted as p(t, T), and the forward rate must be implied by using the forecasting bond price (see https://finpricing.com/lib/FiBond.html), denoted as pfore(t, T). Without any confusion, we may simply call p(t, T) the basis-adjusted bond price. Let us define

 

In an IR term structure model calibration to European swaption market, it is always prefer to have the swaption model price in an analytical close form so that the calibration routine can be effective and accurate. In the LGM calibration, European swaption pricing model prices follows the so-called Jamshidian bond option formula, which has been accepted as market convention for the LGM calibration to the swaption market.


First, we verify that the intrinsic swaption value either by market pricing formula (SABRN model) or by LGM must be consistent with the underlying swap (positive) value. 

Second, we validate that the SABRN model generates correct European swaption value when the pair of basis spread adjusted forecasting and discounting curves are applied. 

Then we ascertain that LGM European swaption close form pricing formula is implemented correctly. We also need to show that LGM numerical (finite difference method) solution to European swaption pricing is consistent with LGM numerical (trinomial tree approach) solution.




