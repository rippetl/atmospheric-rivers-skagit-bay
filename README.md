Master's Thesis work for Lily Rippeteau at Western Washington University.

Data from Skagit Bay and Deception Pass area in Salish Sea, winter 2025-2026 flooding event.


10/5/26

Accidentally broke my code setup with github so here's the code I made to make the new graph and I'll figure out how to fix it all later:

"source": [
    "# try to display salinity at a given height by distance from cast 1\n",
    "cmap = plt.get_cmap('Spectral')\n",
    "colors = cmap(np.linspace(0, 1, 12))\n",
    "\n",
    "coords = [(48.27074548, -122.526624),\n",
    "           (48.33977778, -122.5387838),\n",
    "           (48.33987186, -122.5389417),\n",
    "           (48.36230953, -122.5582912),\n",
    "           (48.38845363, -122.5776857),\n",
    "           (48.38845946, -122.5776799),\n",
    "           (48.4117159, -122.615753),\n",
    "           (48.40895012, -122.6303144),\n",
    "           (48.40531899, -122.6525697),\n",
    "           (48.40531568, -122.6525894),\n",
    "           (48.40531547, -122.6526035),\n",
    "           (48.40678758, -122.694162)]\n",
    "\n",
    "distances = [0]\n",
    "\n",
    "for i in range(1, len(coords)):\n",
    "    dist = ((coords[i][0] - coords[0][0])**2 + (coords[i][1] - coords[0][1])**2)**0.5\n",
    "    distances.append(dist)\n",
    "\n",
    "salinity1 = []\n",
    "salinity2 = []\n",
    "for i, cast in enumerate(cast_list):\n",
    "    closest_idx_pos = np.abs(cast['Salinity'].to_numpy() - 3).argmin()\n",
    "    salinity1.append(cast['Salinity'].iloc[closest_idx_pos])\n",
    "    closest_idx_neg = np.abs(cast['Salinity'].to_numpy() - 12).argmin()\n",
    "    salinity2.append(cast['Salinity'].iloc[closest_idx_neg])\n",
    "\n",
    "plt.plot(distances, salinity1, color='blue', label='About 3m')\n",
    "plt.plot(distances, salinity2, color='red', label='About 12m')\n",
    "\n",
    "plt.xlabel('Distance from Cast 1')\n",
    "plt.ylabel('Salinity (psu)')\n",
    "plt.title('Salinity vs. Distance from Cast 1 at About 3m and About 12m')\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=\"upper left\")\n",
    "plt.show()\n"
