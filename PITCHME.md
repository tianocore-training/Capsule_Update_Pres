---?image=assets/images/gitpitch-audience.jpg
@title[Platform Build Lab]
<br><br><br><br><br>
## <span class="gold"   >UEFI & EDK II Training</span>

#### UEFI Capsule Update

<br>
<span style="font-size:0.75em" ><a href='http://www.tianocore.org'>tianocore.org</a></span>
Note:
  PITCHME.md for UEFI / EDK II Training  Capsule Update Pres

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



---  
@title[Lesson Objective]
<BR>
### <p align="center"<span class="gold"   >Lesson Objective </span></p><br>

<!---  Add bullets using https://fontawesome.com/cheatsheet certificate
-->
<br>
 @fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;What is Capsule Update </span><br>
 @fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Why is Capsule Update needed</span><br>
 @fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;How to enable Capsule Update in Edk II platforms</span> <br>


---?image=assets/images/binary-strings-black2.jpg
@title[UEFI Aware OS Requirements Section]
<br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UEFI Capsule Update Overview</span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>

---
@title[What is Capsule Update Video]


![video](https://www.youtube.com/watch?v=_4P2RQMSu6c&feature=youtu.be)

Note:

Capsule Update is a MORE secure way to update the firmware using a firmware image where the capsule is a file that contains a firmware update image.<br>   
A security benefit is that the capsule update method only works if the existing image on the target system has the same 
signature as used with to build the original  Firmware image currently on the target system.<br> 
When the Capsule update method is enabled, The EDK II Build will generate a firmware image in for form of a capsule or file.  The file will have a .CAP extension. <br> 


The EDK II Build process will also create a UEFI Shell application called “CapsuleAPP.efi” that will use  the capsule file.  <br>
When the Capsule update method is enabled,  the verification method can also be selected for how a firmware update image is verified, or authenticated, before it is used.  The verifications methods are NONE, Test or user generated.<br> 
Image authentication is typically required for shipping products to make sure only valid firmware update images are applied to a specific product.<br> 
When the UEFI Shell application, CapsuleAPP,  is invoked with a .CAP file image, the target system will reboot twice.  The first time to authenticate the firmware update image and update the FLASH device.  The second time to boot using the updated FLASH device.<br> 


 
---?image=/assets/images/slides/Slide5.JPG
<!-- .slide: data-transition="none" -->
@title[Why Capsule Update Needed]
<p align="right"><span class="gold" >Why is Capsule Update Needed?</span></p>
<span style="font-size:0.9em" >Establish a <font color="yellow"> <b>Root-of-Trust</b></font> at the low-level platform initialization</span> <br>
<span style="font-size:0.8em" >National Institute of Standards and Technology (NIST) provides guidelines on BIOS update, 
<a href="http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf">[800-147]  </a></span><br>
<ul>
- <span style="font-size:0.6em" >BIOS Update Authentication</span>
- <span style="font-size:0.6em" >Secure Local Update Method </span>
- <span style="font-size:0.6em" >Integrity Protection</span>
- <span style="font-size:0.6em" >Non-Bypassabilitiy </span>
</ul>
<br>
<br>
<br>
<p align="right"><span style="font-size:0.5em"  >NIST:  <a href="http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf">SP 800-147 .pdf</a></span></p>



Note:

Firmware is responsible for low-level platform initialization and hand-off to the operating system. 

This means firmware establishes root-of-trust for the platform. Signed capsules help assure that the correct update is being applied to the platform. 

Using signed images with UEFI Capsule allows an OS-agnostic process to provide verified firmware updates, utilizing root-of-trust established by the firmware. 

This scenario assumes the factory-provisioned firmware and subsequent updates are signed with the same public/private keypair.


+++?image=/assets/images/slides/Slide6.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Why Capsule Update Needed]
<p align="right"><span class="gold" >Why is Capsule Update Needed?</span></p>
<span style="font-size:0.9em" >Establish a <font color="yellow"> <b>Root-of-Trust</b></font> at the low-level platform initialization</span> <br>
<span style="font-size:0.8em" >National Institute of Standards and Technology (NIST) provides guidelines on BIOS update, 
<a href="http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf">[800-147]  </a></span><br>
<ul>
- <span style="font-size:0.6em" >BIOS Update Authentication</span>
- <span style="font-size:0.6em" >Secure Local Update Method </span>
- <span style="font-size:0.6em" >Integrity Protection</span>
- <span style="font-size:0.6em" >Non-Bypassabilitiy </span>
</ul>
<br>
<br>
<br>
<span style="font-size:0.9em" >Does not describe implementation – the    </span>
<p align="right"><span style="font-size:0.5em"  >NIST:  <a href="http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf">SP 800-147 .pdf</a></span></p>

Note:

Firmware is responsible for low-level platform initialization and hand-off to the operating system. 

This means firmware establishes root-of-trust for the platform. Signed capsules help assure that the correct update is being applied to the platform. 

Using signed images with UEFI Capsule allows an OS-agnostic process to provide verified firmware updates, utilizing root-of-trust established by the firmware. 

This scenario assumes the factory-provisioned firmware and subsequent updates are signed with the same public/private keypair.

---?image=/assets/images/slides/Slide8.JPG
@title[Solving Firmware Update]
<p align="right"><span class="gold" >Solving Firmware Update</span></p>
<br>
<div class="left1">
     <ul>
       <li><span style="font-size:0.8em" >Reliable update story </span></li>
	   <ul>
           <li><span style="font-size:0.7em" >Fault tolerant</span></li>
           <li><span style="font-size:0.7em" >Scalable & repeatable</span></li>
       </ul>
       <li><span style="font-size:0.8em" >How can UEFI Help? </span></li>
       <ul>
           <li><span style="font-size:0.8em" >Capsule model for binary delivery</span></li>
           <li><span style="font-size:0.8em" >Bus / Device Enumeration </span></li>
           <li><span style="font-size:0.8em" >Managing updates via: <br></span><span style="font-size:0.6em" >EFI System Resoure Table, Firmware Management Protocol (FMP) and<br>  Capsule Signing </span></li>
       </ul>
</div>
<div class="right1">
   <p align="center"><span style="font-size:01.2em" ><font color="yellow"></font></span></p>
</div>

Note:

- UEFI open platforms_Vincent.ppt slide 24  - CanSecWest 2015 -  Refrences [6]: https://firmware.intel.com/blog/security-technologies-and-minnowboard-max?page=1



---?image=assets/images/binary-strings-black2.jpg
@title[How does the Capsule Update work? Section]
<br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;How does Capsule Update work?</span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>


---
@title[UEFI Spec defines Capsule Services ]
<br>
<p align="right"><span class="gold" >UEFI Spec defines Capsule Services to meet NIST Requirements</span></p>

- <span style="font-size:0.8em"><b>EFI_FIRMWARE_MANAGEMENT_PROTOCOL</b>, (FMP) capsule format</span> |
- <span style="font-size:0.8em"><b>EFI System Resource Table</b> (ESRT) to support system firmware and device firmware update </span> |
- <span style="font-size:0.8em">An OS agent may call the UEFI service `UpdateCapsule()` to pass the capsule image from the OS to the firmware. Based upon the capsule flags, the 
firmware may process the capsule image immediately, or the firmware may reset the system and process the capsule image on the next boot </span> |

Note:

Same as slide



---?image=/assets/images/slides/Slide12.JPG
@title[UEFI Capsule Update – (FMP)]
<p align="right"><span class="gold" >UEFI Capsule Update – Firmware Management Protocol (FMP)</span></p>


Note:

Source: https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf 


- FMP capsule image format
- Update FMP drivers 
- FMP payloads
    - binary update image and optional vendor code
- The platform may consume a FMP protocol to update the firmware image

 
The FMP capsule image format is shown in This slide. 
It contains the update FMP drivers and the FMP payloads. The FMP payload contains the binary update image and optional vendor code. The platform may consume a FMP protocol to update the firmware image.
 




The UEFI specification [UEFI] defines UEFI capsule services, EFI_FIRMWARE_MANAGEMENT_PROTOCOL, FMP capsule format and EFI System Resource Table (ESRT) to support system firmware and device firmware update.
 
The platform may consume a system FMP and a device FMP protocol to get the firmware image information and report the ESRT to a UEFI OS.
 
An OS agent may call the UEFI service UpdateCapsule() to pass the capsule image from the OS to the firmware. Based upon the capsule flags, the firmware may process the capsule image immediately, or the firmware may reset the system and process the capsule image on the next boot.

---?image=/assets/images/slides/Slide14.JPG
<!-- .slide: data-transition="none" -->
@title[Capsule Update - flow ]
#### <p align="right"><span class="gold" >Capsule Update - flow </span></p>


Note:

Source: https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf 

one possible way is that the operating system sends a firmware image to the system and lets the system update the flash device before the flash device is locked in next boot. This slide.
This firmware image is called a “capsule”. The UEFI specification defines a set of capsule services to let operating system pass the information to the firmware. The UEFI specification also defines the capsule image format for the EFI_FIRMWARE_MANAGEMENT_PROTOCOL (FMP).

EDKII provides the sample drivers to performance the signed system firmware update via the capsule interface. It follows the NIST standard, Microsoft design and the UEFI specification.

+++?image=/assets/images/slides/Slide15.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Capsule Update - flow 02]
#### <p align="right"><span class="gold" >Capsule Update - flow </span></p>


Note:

Source: https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf 

one possible way is that the operating system sends a firmware image to the system and lets the system update the flash device before the flash device is locked in next boot. This slide.
This firmware image is called a “capsule”. The UEFI specification defines a set of capsule services to let operating system pass the information to the firmware. The UEFI specification also defines the capsule image format for the EFI_FIRMWARE_MANAGEMENT_PROTOCOL (FMP).

EDKII provides the sample drivers to performance the signed system firmware update via the capsule interface. It follows the NIST standard, Microsoft design and the UEFI specification.



+++?image=/assets/images/slides/Slide16.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Capsule Update - flow 03]
#### <p align="right"><span class="gold" >Capsule Update - flow </span></p>


Note:

Source: https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf 

one possible way is that the operating system sends a firmware image to the system and lets the system update the flash device before the flash device is locked in next boot. This slide.
This firmware image is called a “capsule”. The UEFI specification defines a set of capsule services to let operating system pass the information to the firmware. The UEFI specification also defines the capsule image format for the EFI_FIRMWARE_MANAGEMENT_PROTOCOL (FMP).

EDKII provides the sample drivers to performance the signed system firmware update via the capsule interface. It follows the NIST standard, Microsoft design and the UEFI specification.


---?image=/assets/images/slides/Slide18.JPG
@title[UEFI Firmware Secure “Capsule” Update]
<p align="right"><span class="gold" >UEFI Firmware Secure “Capsule” Update</span></p>


Note:
Capsule update is a runtime service used to update UEFI FW
<br>
1. Update is initiated by update application/OS runtime
2. Update application stores update “capsule” in DRAM or HDD on ESP (e.g. \EFI\CapsuleUpdate)
3. Upon reboot or S3 resume, FW finds and parses update capsule
4. After FW verifies digital signature of the capsule, FW writes new BIOS FV(s) to SPI flash memory


---?image=/assets/images/slides/Slide20.JPG
@title[Delivering Update “Capsules” in OS]
<p align="right"><span class="gold" >Delivering Update “Capsules” in OS</span></p>


Note:


Source:
https://firmware.intel.com/blog/security-technologies-and-minnowboard-max?page=1 
UEFI open platforms_Vincent.ppt slide 24  - CanSecWest 2015 -  Refrences [6]: reference # [6] Slide 25 of PPT

- UEFI supports Capsule format
- Tools for capsule generation
- Core logic for capsule handling
- Extensible Capsule format
- Self-contained
- Discrete updates
- Composite updates
- Firmware Management Protocol allows 
- Reading / updating firmware
- Integrity checks



---?image=/assets/images/slides/Slide22.JPG
@title[Firmware Update Rollback Protection]
<p align="right"><span class="gold" >Firmware Update Rollback Protection</span></p>


Note:


Source:
https://firmware.intel.com/blog/security-technologies-and-minnowboard-max?page=1 
UEFI open platforms_Vincent.ppt slide 24  - CanSecWest 2015 -  Refrences [6]: reference # [6] Slide 26 of PPT


1. Each version fixes some issues with the previous. Since none are known to have security flaws, each new version allows updates to all older versions.
2. In V4, one of the issues fixed in V3 is realized to be a security fix.  V4 will not allow updates to earlier versions, even V3 since it allows update to V2.
3. Version 5 can now accept only versions 5 and 4.


---?image=assets/images/binary-strings-black2.jpg
@title[How to Enable Capsule Update Section]
<br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;How to Enable?</span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;How to Enable Capsule Update on a  EDK II Platform?</span>


---?image=/assets/images/slides/Slide25.JPG
<!-- .slide: data-transition="none" -->
@title[UEFI Capsule Implementation in EDK II]
<p align="right"><span class="gold" >UEFI Capsule Implementation in EDK II</span></p>
<br>
<span style="font-size:0.9em" ><a href="https://github.com/tianocore/edk2/tree/master/SignedCapsulePkg">SignedCapsulePkg </a> Uses <a href="https://www.openssl.org/"> OpenSSL</a>to sign and authenticate firmware update capsules and firmware recovery images
</span>

Note:

- Test signing key 
   - used for firmware development and debug
- Production signing key 
   - used by OEM to create and manage their own 
- OpenSLL utilities can be used to create key


+++?image=/assets/images/slides/Slide26.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[UEFI Capsule Implementation in EDK II]
<p align="right"><span class="gold" >UEFI Capsule Implementation in EDK II</span></p>
<br>
<span style="font-size:0.9em" ><a href="https://github.com/tianocore/edk2/tree/master/SignedCapsulePkg">SignedCapsulePkg </a> Uses <a href="https://www.openssl.org/"> OpenSSL</a>to sign and authenticate firmware update capsules and firmware recovery images
</span>

Note:

- Test signing key 
   - used for firmware development and debug
- Production signing key 
   - used by OEM to create and manage their own 
- OpenSLL utilities can be used to create key


---
@title[Enable Capsule Based System Firmware Update]
<p align="right"><span class="gold" >Enable Capsule Based System Firmware Update</span></p>
<br>
<span style="font-size:0.9em" >The following wiki pages provide details on how to add the system firmware update using Signed UEFI Capsules </span>
<br>
- <span style="font-size:0.8em" >Implement Platform Components for UEFI Capsule : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Capsule-Based-System-Firmware-Update-Implementation">link</a> </span>
- <span style="font-size:0.8em" >Add <font face="Courier New">CAPSULE_ENABLE</font> feature to Platform DSC/FDF Files : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Capsule-Based-System-Firmware-Update-DSC-FDF">link</a></span>
- <span style="font-size:0.8em" >Verify <font face="Courier New">CAPSULE_ENABLE</font> feature using Test Signing Keys : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Capsule-Based-System-Firmware-Update-Verify-Test-Keys">link</a></span>
- <span style="font-size:0.8em" >Change System Firmware Update Version : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Change-System-Firmware-Update-Version">link</a></span>
- <span style="font-size:0.8em" >Change <font face="Courier New">ESRT</font> System Firmware Update GUID : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Change-ESRT-System-Firmware-Update-GUID">link</a></span>
- <span style="font-size:0.8em" >How to Generate Signing Keys using OpenSSL Command Line Utilities : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Capsule-Based-System-Firmware-Update-Generate-Keys">link</a></span>
- <span style="font-size:0.8em" >Verify <font face="Courier New">CAPSULE_ENABLE</font> feature using Generated Signing Keys : <a href="https://github.com/tianocore/tianocore.github.io/wiki/Capsule-Based-System-Firmware-Update-Verify-Generated-Keys">link</a></span>


Note:

Same as slide


---?image=/assets/images/slides/Slide29.JPG
<!-- .slide: data-transition="none" -->
@title[Implement Platform Components for UEFI Capsule]
<p align="right"><span class="gold" >Implement Platform Components for UEFI Capsule</span></p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="right"><span style="font-size:0.6em" >Example from Minnowboard Max/Turbot platform: <a href="https://github.com/tianocore/edk2-platforms/tree/devel-MinnowBoardMax-UDK2017/Vlv2TbltDevicePkg/Feature/Capsule">github link</a></span></p>

Note:

#### Library
In order for a signed capsule to update the non-volatile storage device that that contains the system firmware contents that may be updated, an instance of the PlatformFlashAccessLib must be implemented. This library class provides a single API to update a portion of the non-volatile storage device.

#### Descriptor
The System Firmware Descriptor information is implemented in the file SystemFirmwareDescriptor.aslc. The version and string information must be updated for the system firmware update requirements. The IMAGE_TYPE_ID_GUID define must be set to a new GUID value(using C structure syntax) for the platform. This GUID value must be one of the GUID values the platform supports for Capsule Base System Firmware Updates. The PCD called gEfiMdeModulePkgTokenSpaceGuid.PcdSystemFmpCapsuleImageTypeIdGuid is set to an array of one or more of IMAGE_TYPE_ID_GUID values (using byte array syntax) in the Platform DSC file described 

#### Config Ini file:
his a System Firmware Update Configuration INI file provides the inventory of components in a capsule that are used by the system firmware's Firmware Management Protocol to update one or more components in the system firmware's non-volatile storage device using the PlatformFlashAccessLib instance implemented in the step above.
The INI file is ASCII text. The first section is [Head]. The value of NumHeadUpdate must be set to the number of components in the inventory. There must be an UpdateX statement assigned to a unique name for each component in the inventory.



+++?image=/assets/images/slides/Slide30.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Implement Platform Components for UEFI Capsule 02]
<p align="right"><span class="gold" >Implement Platform Components for UEFI Capsule</span></p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="right"><span style="font-size:0.6em" >Example from Minnowboard Max/Turbot platform: <a href="https://github.com/tianocore/edk2-platforms/tree/devel-MinnowBoardMax-UDK2017/Vlv2TbltDevicePkg/Feature/Capsule">github link</a></span></p>

Note:

#### Library
In order for a signed capsule to update the non-volatile storage device that that contains the system firmware contents that may be updated, an instance of the PlatformFlashAccessLib must be implemented. This library class provides a single API to update a portion of the non-volatile storage device.

#### Descriptor
The System Firmware Descriptor information is implemented in the file SystemFirmwareDescriptor.aslc. The version and string information must be updated for the system firmware update requirements. The IMAGE_TYPE_ID_GUID define must be set to a new GUID value(using C structure syntax) for the platform. This GUID value must be one of the GUID values the platform supports for Capsule Base System Firmware Updates. The PCD called gEfiMdeModulePkgTokenSpaceGuid.PcdSystemFmpCapsuleImageTypeIdGuid is set to an array of one or more of IMAGE_TYPE_ID_GUID values (using byte array syntax) in the Platform DSC file described 

#### Config Ini file:
his a System Firmware Update Configuration INI file provides the inventory of components in a capsule that are used by the system firmware's Firmware Management Protocol to update one or more components in the system firmware's non-volatile storage device using the PlatformFlashAccessLib instance implemented in the step above.
The INI file is ASCII text. The first section is [Head]. The value of NumHeadUpdate must be set to the number of components in the inventory. There must be an UpdateX statement assigned to a unique name for each component in the inventory.

+++?image=/assets/images/slides/Slide31.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Implement Platform Components for UEFI Capsule 03]
<p align="right"><span class="gold" >Implement Platform Components for UEFI Capsule</span></p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="right"><span style="font-size:0.6em" >Example from Minnowboard Max/Turbot platform: <a href="https://github.com/tianocore/edk2-platforms/tree/devel-MinnowBoardMax-UDK2017/Vlv2TbltDevicePkg/Feature/Capsule">github link</a></span></p>

Note:

#### Library
In order for a signed capsule to update the non-volatile storage device that that contains the system firmware contents that may be updated, an instance of the PlatformFlashAccessLib must be implemented. This library class provides a single API to update a portion of the non-volatile storage device.

#### Descriptor
The System Firmware Descriptor information is implemented in the file SystemFirmwareDescriptor.aslc. The version and string information must be updated for the system firmware update requirements. The IMAGE_TYPE_ID_GUID define must be set to a new GUID value(using C structure syntax) for the platform. This GUID value must be one of the GUID values the platform supports for Capsule Base System Firmware Updates. The PCD called gEfiMdeModulePkgTokenSpaceGuid.PcdSystemFmpCapsuleImageTypeIdGuid is set to an array of one or more of IMAGE_TYPE_ID_GUID values (using byte array syntax) in the Platform DSC file described 

#### Config Ini file:
his a System Firmware Update Configuration INI file provides the inventory of components in a capsule that are used by the system firmware's Firmware Management Protocol to update one or more components in the system firmware's non-volatile storage device using the PlatformFlashAccessLib instance implemented in the step above.
The INI file is ASCII text. The first section is [Head]. The value of NumHeadUpdate must be set to the number of components in the inventory. There must be an UpdateX statement assigned to a unique name for each component in the inventory.

+++?image=/assets/images/slides/Slide32.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Implement Platform Components for UEFI Capsule 04]
<p align="right"><span class="gold" >Implement Platform Components for UEFI Capsule</span></p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="right"><span style="font-size:0.6em" >Example from Minnowboard Max/Turbot platform: <a href="https://github.com/tianocore/edk2-platforms/tree/devel-MinnowBoardMax-UDK2017/Vlv2TbltDevicePkg/Feature/Capsule">github link</a></span></p>

Note:

#### Library
In order for a signed capsule to update the non-volatile storage device that that contains the system firmware contents that may be updated, an instance of the PlatformFlashAccessLib must be implemented. This library class provides a single API to update a portion of the non-volatile storage device.

#### Descriptor
The System Firmware Descriptor information is implemented in the file SystemFirmwareDescriptor.aslc. The version and string information must be updated for the system firmware update requirements. The IMAGE_TYPE_ID_GUID define must be set to a new GUID value(using C structure syntax) for the platform. This GUID value must be one of the GUID values the platform supports for Capsule Base System Firmware Updates. The PCD called gEfiMdeModulePkgTokenSpaceGuid.PcdSystemFmpCapsuleImageTypeIdGuid is set to an array of one or more of IMAGE_TYPE_ID_GUID values (using byte array syntax) in the Platform DSC file described 

#### Config Ini file:
his a System Firmware Update Configuration INI file provides the inventory of components in a capsule that are used by the system firmware's Firmware Management Protocol to update one or more components in the system firmware's non-volatile storage device using the PlatformFlashAccessLib instance implemented in the step above.
The INI file is ASCII text. The first section is [Head]. The value of NumHeadUpdate must be set to the number of components in the inventory. There must be an UpdateX statement assigned to a unique name for each component in the inventory.

---?image=/assets/images/slides/Slide34.JPG
@title[Add CAPSULE_ENABLE feature ]
<p align="right"><span class="gold" >Add `CAPSULE_ENABLE` feature to Platform DSC/FDF Files</span></p>
<div class="left2">
     <ul>
       <li><span style="font-size:0.8em" >Add `-D CAPSULE_ENABLE` to the build command line to enable capsule update features. </span></li>
       <li><span style="font-size:0.8em" >The build process generates a capsule update image (.cap file) along with the UEFI application `CapsuleApp.efi`. </span></li>
	   <ul>
           <li><span style="font-size:0.7em" >Copy `.cap` file and `CapsuleApp.efi` to USB thumb drive</span></li>
           <li><span style="font-size:0.7em" >Boot to UEFI Shell and use `CapsuleApp.efi` with `.cap` signed capsule file</span></li>
       </ul>
       <li><span style="font-size:0.8em" >Once the system is rebooted, the signed capsule is authenticated and the firmware is update with the new system firmware version. </span></li>
</div>
<div class="right2">
   <p align="center"><span style="font-size:01.2em" ><font color="yellow"></font></span></p>
</div>

Note:

- Add -D CAPSULE_ENABLE to the build command line to enable capsule update features.
- The build process generates a capsule update image (.cap file) along with the UEFI application CapsuleApp.efi.  
- These 2 files must be transferred to storage media to in order for a user to boot to UEFI Shell and use CapsuleApp.efi to submit the signed capsule. Once the system is rebooted, the signed capsule is authenticated and the firmware is update with the new system firmware version.
<br>
- Platform DSC Sections:
   - [LibraryClasses]
   - [Pcds]
   - [Components]
- Platform FDF Sections:
   - [FV] PEI 
   - [FV] DXE
   - [FV] Platform
   - [VmpPayload]
   - [Capsule]
   - [Rule]


---?image=/assets/images/slides/Slide36.JPG
@title[Verify CAPSULE_ENABLE Feature  ]
<p align="right"><span class="gold" >Verify `CAPSULE_ENABLE` Feature using Test Signing Keys</span></p>
<div class="left">
     <ul>
       <li><span style="font-size:0.8em" >Download the OpenSSL library</span></li>
       <li><span style="font-size:0.8em" >Build the Boot Firmware image with `CAPSULE_ENABLE`</span></li>
       <li><span style="font-size:0.8em" >Copy the `CapsuleApp.efi` to USB thumb drive and run on Target system</span></li>
</div>
<div class="right">
   <p align="center"><span style="font-size:01.2em" ><font color="yellow"></font></span></p>
</div>

Note:

- Download the OpenSSL library 
- Build the Boot Firmware image with CAPSULE_ENABLE
- Copy the CapsuleApp.efi to USB thumb drive and run on Target system

---?image=/assets/images/slides/Slide38.JPG
@title[Verify Capsule Enable -P ]
<br>
<p align="right"><span class="gold" >Verify `CAPSULE_ENABLE`  with `CapsuleApp -P` option</span></p>

Note:


---?image=/assets/images/slides/Slide39.JPG
@title[Verify Capsule Enable -E ]
<br>
<p align="right"><span class="gold" >Verify `CAPSULE_ENABLE`  with `CapsuleApp -E` option</span></p>

Note:



---  
@title[Summary]
<BR>
### <p align="center"><span class="gold"   >Summary </span></p><br>
<br>
 @fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;What is Capsule Update </span><br>
 @fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Why is Capsule Update needed</span><br>
 @fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;How to enable Capsule Update in Edk II platforms</span> <br>

 

---?image=assets/images/gitpitch-audience.jpg
@title[Questions]
<br>
![Questions](/assets/images/Questions.png =10x) 


---?image=assets/images/gitpitch-audience.jpg
@title[Logo Slide]
<br><br><br>
![Logo Slide](/assets/images/TianocoreLogo.png =10x)


---
@title[Acknowledgements]
#### <p align="center"><span class="gold"   >Acknowledgements</span></p>

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2018, Intel Corporation. All rights reserved.
**/

```
