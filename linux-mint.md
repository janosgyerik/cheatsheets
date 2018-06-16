Restart X server:

    sudo restart mdm

Restart USB:

    # lspci | grep -i usb
    00:14.0 USB controller: Intel Corporation Wildcat Point-LP USB xHCI Controller (rev 03)
    00:1d.0 USB controller: Intel Corporation Wildcat Point-LP USB EHCI Controller (rev 03)

    printf "0000:00:14.0" | tee /sys/bus/pci/drivers/xhci_hcd/unbind
    printf "0000:00:14.0" | tee /sys/bus/pci/drivers/xhci_hcd/bind
    
    
