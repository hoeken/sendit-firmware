# v2.7

* add graphs for each channel
    * firmware side
        * make a class for it? dont bake it into ADCChannel
        * store history in psram
        * etl::circular_buffer (uint32_t timestamp, float value)
        * 2^14 points / 1 per minute = 11.37 days
        * 2^14 seconds  = 4.55 hours
        * in ADCController add a page /graphdata
            * id=?? GET param
            * loop through circular buffer in chunks (512 / 1024)
            * request.sendHeader("Content-Type", "application/octet-stream");
            * write as raw data to the request
    * client side 
        * history via arrayBuffer / DataView
        * updates via get_graph_data every xxx ms
        * uplot or Chart.js for the library
        * open a graph overlay when user clicks on the adc card
        * how to handle date ranges / parsing data?  say we have 11 days of data...