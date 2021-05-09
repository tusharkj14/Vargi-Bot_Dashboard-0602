# This Documentation covers the working of the IoT py file

## Function for updating inventory sheet

    -   update_inventory(arg_colorlist):
        
        This function appends the inventory sheet
        of the inventory management spreadsheet.
        The sorted colors list is passed and
        are appended in the sheet as required
        
        Parameters:
            type arg_colorlist: list of strings
                        A python list containing the different colours of all packages
   

## Function for updating incoming orders sheet

    -   update_incoming(arg_list):
        
        This function appends the IncomingOrders sheet
        of the inventory management spreadsheet.
        
        Parameters:
            type arg_list: list of strings
                    A python list containing the order details that are fetched

## Function for updating dispatched orders sheet

    -   update_dispatch(arg_list):
        
        This function appends the OrdersDispatched sheet
    of the inventory management spreadsheet.
        
        Parameters:
            type arg_list: list of strings
                    A python list containing the order details that are fetched
    

## Function for updating shipped orders sheet

    -   update_shipped(arg_list):
        
        This function appends the OrdersShipped sheet
        of the inventory management spreadsheet.
        
        Parameters:
            type arg_list: list of strings
                    A python list containing the order details that are fetched
        
