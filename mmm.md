/*CALL createCity("Hanoi");
Call createCityCenter("Hanoi","HCM_quan2");
call createCityCenterCourt("HCM","HCM_quan1","Court#1");
call createplayer("customer#A");
call createStaff("Staff#1","HCM_quan1","HCM");
# CancelBooking (CA) parameters: booking_id, customer_id
-- CA-001: customer not exist
Call CancelBooking('1', 'Customer#A');
-- CA-002: booking not exist
Call CancelBooking('12', 'Customer#B');
-- CA-003: this customer not own the booking
Call CancelBooking('1', 'Customer#B');
-- CA-004: violates 24 hours before start time
Call CancelBooking('11', 'E');
-- CP-001: staff not exist
CALL updateBookingStatus(0 ,'1', 'HCM','HCM_quan1','Staff#6');
-- CP-002: booking not exist
CALL updateBookingStatus(0 ,'12', 'Hanoi','HCM_quan2','Staff#1');
-- CP-003: this staff has no relationship with the booking (join booking - court - center - staff)
CALL updateBookingStatus(0 ,'1', 'Can_tho','HCM_quan1','Staff#3' );
-- staff
-- INSERT INTO staff (staff_id,`center_id`,`city_id`) VALUES ('Staff#1','HCM_quan1','HCM');
-- INSERT INTO staff (staff_id,`center_id`,`city_id`) VALUES ('Staff#2','HCM_quan2','Hanoi');
-- INSERT INTO staff (staff_id,`center_id`,`city_id`) VALUES ('Staff#3','HCM_quan3','Can_Tho');
-- INSERT INTO staff (staff_id,`center_id`,`city_id`) VALUES ('Staff#4','HCM_quan4','HCM');
-- INSERT INTO staff (staff_id,`center_id`,`city_id`) VALUES ('Staff#5','HCM_quan5','HCM');*/
	CALL CreateBooking(13, "2020-03-29 09:27:18", "2020-02-01", 10, 10, 18, 35, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
-- CB-002: startTime < openTime 
	CALL CreateBooking(14, "2020-03-29 09:27:18", "2020-05-01", 6, 10, 18, 35, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
-- CB-003: endTime > closeTime 
	CALL CreateBooking(15, "2020-03-29 09:27:18", "2020-04-15", 9, 00, 23, 00, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
-- CB-004: endTime < startTime
	CALL CreateBooking(16, "2020-03-29 09:27:18", "2020-04-16", 9, 00, 8, 00, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
-- CB-005: playtime invalid (valid: 45m, 1h, 1h15m, 1h30m)
	CALL CreateBooking(17, "2020-03-29 09:27:18", "2020-04-17", 9, 00, 9, 35, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
-- CB-006: overlapping booking
--       9:00===========10:00  existed booking
--    8:00========9:30
--           9:30==============10:30
--           9:15==10:00
--    8:30============10:00

	CALL CreateBooking(18, "2020-03-29 09:27:18", "2020-04-18", 9, 00, 9, 35, 'HCM', 'HCM_quan1', 'Court#1', 'Customer#A');
	CALL CreateBooking("2020-04-01", 9, 30, 10, 30, 4, 997, "2020-03-29 09:27:18");
	CALL CreateBooking("2020-04-01", 9, 15, 10, 0, 4, 997, "2020-03-29 09:27:18");
	CALL CreateBooking("2020-04-01", 8, 30, 10, 0, 4, 997, "2020-03-29 09:27:18");

-- CB-007: have pending booking
	CALL CreateBooking("2020-03-30", 17, 0, 18, 0, 4, 1, "2020-03-29 09:27:18");
-- CB-008: no more than 3 bookings
	CALL CreateBooking("2020-04-01", 17, 0, 18, 0, 4, 999, "2020-03-29 09:27:18");
-- CB-109: Customer not existed.
	CALL CreateBooking("2020-04-02", 17, 0, 18, 0, 4, 404, "2020-03-29 09:27:18");
-- CB-110: Court not existed.
	CALL CreateBooking("2020-04-03", 17, 0, 18, 0, 404, 2, "2020-03-29 09:27:18");
-- CB-111: Court & Customer not existed.
	CALL CreateBooking("2020-04-03", 17, 0, 18, 0, 404, 404, "2020-03-29 09:27:18");
