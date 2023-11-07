# Fetch Properties From Yml

Project: UIA
Date Added: November 6, 2023
Description: Yml to code main kaise properties lete hai
ID: SPT-1
Status: Added

![Untitled](Fetch%20Properties%20From%20Yml%200e83f4375a1d406fb1f7fce89b59593e/Untitled.png)

```java
@Component
@ConfigurationProperties(prefix = "jobmanagerservice")
public class JobManagerServiceConfiguration {

	private String ezxchangehost;
	private String ezxchangeport;

	public String getEzxchangehost() {
		return ezxchangehost;
	}

	public void setEzxchangehost(String ezxchangehost) {
		this.ezxchangehost = Prerequisites.checkNotEmpty(ezxchangehost, "ezxchangehost");
	}

	public String getEzxchangeport() {
		return ezxchangeport;
	}

	public void setEzxchangeport(String ezxchangeport) {
		this.ezxchangeport = Prerequisites.checkNotEmpty(ezxchangeport, "ezxchangeport");
	}

}
```

```java

private String getServerURL() {
        return new StringBuilder()
            .append(ServiceConstants.HTTP)
            .append(gatewayHost)
            .append(":") //$NON-NLS-1$
            .append(gatewayPort)
            .toString();
    }

String getJobStatusURI = String.format("%s%s", //$NON-NLS-1$
					configurationPropertiesManager.getUri(), configurationPropertiesManager.getGetstatusendpoint());

			UriComponentsBuilder builder = UriComponentsBuilder.fromHttpUrl(getJobStatusURI).queryParam("requestId", //$NON-NLS-1$
					request.getId());
```