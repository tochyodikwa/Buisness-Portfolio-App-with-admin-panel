# Buisness-Portfolio-App-with-admin-panel

import com.csform.businessportfolio.model.Categories;
import com.csform.businessportfolio.model.Clients;
import com.csform.businessportfolio.model.OurTeams;
import com.google.gson.Gson;
import com.google.gson.JsonIOException;
import com.google.gson.JsonSyntaxException;

public class SyncDataHelper {
//Replace with your own base url
//Custom Admin panel not available for this build
	private static final int CONNECTION_TIMEOUT = 45 * 1000; // 45 seconds
	public static final String URL_ROOT = "http://www.pengaja.com/business/admin/index.php/";
	public static final String URL_UPLOADS = "http://pengaja.com/business/admin/uploads/";

	private static BufferedReader getInputStream(String urlString)
			throws IOException {
		urlString = urlString.replaceAll(" ", "%20");
		URL url = new URL(urlString);
		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
		conn.setConnectTimeout(CONNECTION_TIMEOUT);
		return new BufferedReader(new InputStreamReader(conn.getInputStream()));
	}

	public static Clients fetchClients() throws JsonSyntaxException,
			JsonIOException, IOException {
		String urlString = URL_ROOT + "clients/api";
		BufferedReader in = getInputStream(urlString);
		try {
			return new Gson().fromJson(in, Clients.class);
		} finally {
			closeReader(in);
		}
	}