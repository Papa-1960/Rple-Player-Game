package roleplayer;

public class Player {
    private String name;
    private String status;
    private int experience;
    private int level;
    private int currentHitPoints;
    private int maxHitPoints;
    private int damagePoints;

    // Constructor
    public Player(String name, int experience, int currentHitPoints) {
        this.name = name;
        this.experience = experience;
        this.currentHitPoints = currentHitPoints;
        this.level = calculateLevel(experience);
        this.maxHitPoints = calculateMaxHitPoints(level);
        this.damagePoints = calculateDamagePoints(level);
        this.status = "alive";
    }

    // Getters and Setters

    public String getName() {
        return name;
    }

    public String getStatus() {
        return status;
    }

    public int getExperience() {
        return experience;
    }

    public int getLevel() {
        return level;
    }

    public int getCurrentHitPoints() {
        return currentHitPoints;
    }

    public int getMaxHitPoints() {
        return maxHitPoints;
    }

    public int getDamagePoints() {
        return damagePoints;
    }

    public void setExperience(int experience) {
        this.experience = experience;
        this.level = calculateLevel(experience);
        this.maxHitPoints = calculateMaxHitPoints(level);
        this.damagePoints = calculateDamagePoints(level);
    }

    public void setCurrentHitPoints(int currentHitPoints) {
        this.currentHitPoints = currentHitPoints;
        if (currentHitPoints <= 0) {
            this.status = "dead";
        }
    }

    public void setStatus(String status) {
        this.status = status;
    }

    // Helper methods for calculating level, maxHitPoints, and damagePoints

    private int calculateLevel(int experience) {
        int level = experience / 100;
        if (level < 1) {
            return 1;
        }
        return level;
    }

    private int calculateMaxHitPoints(int level) {
        return (int) (level * 100 * (1 + level / 10.0));
    }

    private int calculateDamagePoints(int level) {
        return level * 30;
    }

    // Battle method
    public void battle(Player opponent) {
        int opponentDamage = opponent.getDamagePoints();
        int playerDamage = this.getDamagePoints();

        opponent.setCurrentHitPoints(opponent.getCurrentHitPoints() - playerDamage);
        this.setCurrentHitPoints(this.getCurrentHitPoints() - opponentDamage);

        // After the battle, both players gain 50 experience points
        opponent.setExperience(opponent.getExperience() + 50);
        this.setExperience(this.getExperience() + 50);
    }

    // toString method
    @Override
    public String toString() {
        return "Name: " + name +
               "\nStatus: " + status +
               "\nExperience: " + experience +
               "\nLevel: " + level +
               "\nCurrent Hit Points: " + currentHitPoints +
               "\nMax Hit Points: " + maxHitPoints +
               "\nDamage Points: " + damagePoints;
    }

    // Main method for testing
    public static void main(String[] args) {
        Player player1 = new Player("FiFi", 450, 10000);
        Player player2 = new Player("Moblin", 230, 190);

        System.out.println("Before the battle:");
        System.out.println(player1);
        System.out.println(player2);

        System.out.println(player1.getName() + " is battling " + player2.getName());
        player1.battle(player2);

        System.out.println("After the battle");
        System.out.println(player1);
        System.out.println(player2);

        System.out.println("Battle again");
        player1.battle(player2);

        System.out.println("After the battle");
        System.out.println(player1);
        System.out.println(player2);
    }
}

